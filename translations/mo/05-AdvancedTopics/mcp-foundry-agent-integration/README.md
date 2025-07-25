<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "0d29a939f59d34de10d14433125ea8f5",
  "translation_date": "2025-07-02T10:10:27+00:00",
  "source_file": "05-AdvancedTopics/mcp-foundry-agent-integration/README.md",
  "language_code": "mo"
}
-->
# Model Context Protocol (MCP) 與 Azure AI Foundry 整合

本指南示範如何將 Model Context Protocol (MCP) 伺服器與 Azure AI Foundry 代理整合，實現強大的工具協同與企業級 AI 能力。

## 介紹

Model Context Protocol (MCP) 是一個開放標準，讓 AI 應用能安全地連接外部資料來源與工具。與 Azure AI Foundry 整合後，MCP 使代理能以標準化方式存取並互動各種外部服務、API 及資料來源。

此整合結合 MCP 工具生態系的彈性與 Azure AI Foundry 穩健的代理框架，提供具高度客製化能力的企業級 AI 解決方案。

**Note:** 若想在 Azure AI Foundry Agent Service 使用 MCP，目前僅支援以下區域：westus、westus2、uaenorth、southindia 及 switzerlandnorth

## 學習目標

完成本指南後，您將能夠：

- 了解 Model Context Protocol 及其優勢
- 設定 MCP 伺服器以供 Azure AI Foundry 代理使用
- 建立並配置具 MCP 工具整合的代理
- 使用真實 MCP 伺服器實作實用範例
- 處理代理對話中的工具回應與引用

## 前置條件

開始前請確保您具備：

- 擁有 Azure 訂閱並可使用 AI Foundry
- Python 3.10 以上版本
- 已安裝並設定 Azure CLI
- 具備建立 AI 資源的適當權限

## 什麼是 Model Context Protocol (MCP)？

Model Context Protocol 是 AI 應用連接外部資料來源與工具的標準化方式。主要優點包括：

- **標準化整合**：不同工具與服務間具一致介面
- **安全性**：安全的身份驗證與授權機制
- **彈性**：支援多種資料來源、API 與自訂工具
- **擴充性**：輕鬆新增新功能與整合

## 在 Azure AI Foundry 設定 MCP

### 1. 環境設定

首先，設定環境變數與相依套件：

```python
import os
import time
import json
from azure.ai.agents.models import MessageTextContent, ListSortOrder
from azure.ai.projects import AIProjectClient
from azure.identity import DefaultAzureCredential


### 1. Initialize the AI Project Client

```python
project_client = AIProjectClient(
    endpoint="https://your-project-endpoint.services.ai.azure.com/api/projects/your-project",
    credential=DefaultAzureCredential(),
)
```

### 2. Create an Agent with MCP Tools

Configure an agent with MCP server integration:

```python
with project_client:
    agent = project_client.agents.create_agent(
        model="gpt-4.1-nano", 
        name="mcp_agent", 
        instructions="You are a helpful assistant. Use the tools provided to answer questions. Be sure to cite your sources.",
        tools=[
            {
                "type": "mcp",
                "server_label": "microsoft_docs",
                "server_url": "https://learn.microsoft.com/api/mcp",
                "require_approval": "never"
            }
        ],
        tool_resources=None
    )
    print(f"Created agent, agent ID: {agent.id}")
```

## MCP Tool Configuration Options

When configuring MCP tools for your agent, you can specify several important parameters:

### Configuration

```python
mcp_tool = {
    "type": "mcp",
    "server_label": "unique_server_name",      # MCP 伺服器的識別名稱
    "server_url": "https://api.example.com/mcp", # MCP 伺服器端點
    "require_approval": "never"                 # 核准政策：目前僅支援 "never"
}
```

## Complete Example: Using Microsoft Learn MCP Server

Here's a complete example that demonstrates creating an agent with MCP integration and processing a conversation:

```python
import time
import json
import os
from azure.ai.agents.models import MessageTextContent, ListSortOrder
from azure.ai.projects import AIProjectClient
from azure.identity import DefaultAzureCredential

def create_mcp_agent_example():

    project_client = AIProjectClient(
        endpoint="https://your-endpoint.services.ai.azure.com/api/projects/your-project",
        credential=DefaultAzureCredential(),
    )

    with project_client:
        # 建立具 MCP 工具的代理
        agent = project_client.agents.create_agent(
            model="gpt-4.1-nano", 
            name="documentation_assistant", 
            instructions="You are a helpful assistant specializing in Microsoft documentation. Use the Microsoft Learn MCP server to search for accurate, up-to-date information. Always cite your sources.",
            tools=[
                {
                    "type": "mcp",
                    "server_label": "mslearn",
                    "server_url": "https://learn.microsoft.com/api/mcp",
                    "require_approval": "never"
                }
            ],
            tool_resources=None
        )
        print(f"Created agent, agent ID: {agent.id}")    
        
        # 建立對話串
        thread = project_client.agents.threads.create()
        print(f"Created thread, thread ID: {thread.id}")

        # 傳送訊息
        message = project_client.agents.messages.create(
            thread_id=thread.id, 
            role="user", 
            content="What is .NET MAUI? How does it compare to Xamarin.Forms?",
        )
        print(f"Created message, message ID: {message.id}")

        # 執行代理
        run = project_client.agents.runs.create(thread_id=thread.id, agent_id=agent.id)
        
        # 輪詢完成狀態
        while run.status in ["queued", "in_progress", "requires_action"]:
            time.sleep(1)
            run = project_client.agents.runs.get(thread_id=thread.id, run_id=run.id)
            print(f"Run status: {run.status}")

        # 檢視執行步驟與工具呼叫
        run_steps = project_client.agents.run_steps.list(thread_id=thread.id, run_id=run.id)
        for step in run_steps:
            print(f"Run step: {step.id}, status: {step.status}, type: {step.type}")
            if step.type == "tool_calls":
                print("Tool call details:")
                for tool_call in step.step_details.tool_calls:
                    print(json.dumps(tool_call.as_dict(), indent=2))

        # 顯示對話內容
        messages = project_client.agents.messages.list(thread_id=thread.id, order=ListSortOrder.ASCENDING)
        for data_point in messages:
            last_message_content = data_point.content[-1]
            if isinstance(last_message_content, MessageTextContent):
                print(f"{data_point.role}: {last_message_content.text.value}")

        return agent.id, thread.id

if __name__ == "__main__":
    create_mcp_agent_example()


## 常見問題排解

### 1. 連線問題
- 確認 MCP 伺服器 URL 可連線
- 檢查身份驗證憑證
- 確保網路連線正常

### 2. 工具呼叫失敗
- 檢視工具參數與格式是否正確
- 確認伺服器特定需求
- 實作適當的錯誤處理

### 3. 效能問題
- 優化工具呼叫頻率
- 適當實作快取機制
- 監控伺服器回應時間

## 後續步驟

進一步強化您的 MCP 整合：

1. **探索自訂 MCP 伺服器**：為專有資料來源打造專屬 MCP 伺服器
2. **實作進階安全性**：加入 OAuth2 或自訂認證機制
3. **監控與分析**：實作工具使用的日誌與監控
4. **擴展解決方案**：考慮負載平衡與分散式 MCP 伺服器架構

## 附加資源

- [Azure AI Foundry 文件](https://learn.microsoft.com/azure/ai-foundry/)
- [Model Context Protocol 範例](https://learn.microsoft.com/azure/ai-foundry/agents/how-to/tools/model-context-protocol-samples)
- [Azure AI Foundry 代理概覽](https://learn.microsoft.com/azure/ai-foundry/agents/)
- [MCP 規範](https://spec.modelcontextprotocol.io/)

## 支援

如需額外支援與問題協助：
- 查看 [Azure AI Foundry 文件](https://learn.microsoft.com/azure/ai-foundry/)
- 查閱 [MCP 社群資源](https://modelcontextprotocol.io/)

## 下一步

- [6. 社群貢獻](../../06-CommunityContributions/README.md)

**免責聲明**：  
本文件係使用 AI 翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 進行翻譯。雖然我們致力於確保準確性，但請注意自動翻譯可能包含錯誤或不準確之處。原始文件的母語版本應被視為權威來源。對於重要資訊，建議使用專業人工翻譯。因使用本翻譯所產生之任何誤解或誤釋，本公司概不負責。