<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "315ecce765d22639b60dbc41344c8533",
  "translation_date": "2025-07-09T23:02:40+00:00",
  "source_file": "03-GettingStarted/01-first-server/README.md",
  "language_code": "ne"
}
-->
### -2- परियोजना सिर्जना गर्नुहोस्

अब जब तपाईंले आफ्नो SDK स्थापना गर्नुभएको छ, आउनुहोस् अर्को परियोजना सिर्जना गरौं:

### -3- परियोजना फाइलहरू सिर्जना गर्नुहोस्

### -4- सर्भर कोड सिर्जना गर्नुहोस्

### -5- एउटा उपकरण र स्रोत थप्दै

तलको कोड थपेर एउटा उपकरण र स्रोत थप्नुहोस्:

### -6 अन्तिम कोड

सर्भर सुरु गर्न आवश्यक अन्तिम कोड थपौं:

### -7- सर्भर परीक्षण गर्नुहोस्

तलको आदेश प्रयोग गरेर सर्भर सुरु गर्नुहोस्:

### -8- इन्स्पेक्टर प्रयोग गरेर चलाउनुहोस्

इन्स्पेक्टर एउटा उत्कृष्ट उपकरण हो जसले तपाईंको सर्भर सुरु गर्छ र तपाईंलाई यससँग अन्तरक्रिया गर्न दिन्छ ताकि तपाईं परीक्षण गर्न सक्नुहोस् कि यो काम गर्छ कि गर्दैन। आउनुहोस् यसलाई सुरु गरौं:
> [!NOTE]  
> यो "command" फिल्डमा फरक देखिन सक्छ किनभने यसमा तपाईंको विशेष runtime सँग सर्भर चलाउने कमाण्ड हुन्छ/
तपाईंले निम्न प्रयोगकर्ता इन्टरफेस देख्नुपर्छ:

![Connect](../../../../translated_images/connect.141db0b2bd05f096fb1dd91273771fd8b2469d6507656c3b0c9df4b3c5473929.ne.png)

1. Connect बटन चयन गरेर सर्भरमा जडान गर्नुहोस्  
  सर्भरमा जडान भएपछि, तपाईंले अब निम्न देख्नुपर्छ:

  ![Connected](../../../../translated_images/connected.73d1e042c24075d386cacdd4ee7cd748c16364c277d814e646ff2f7b5eefde85.ne.png)

1. "Tools" र "listTools" चयन गर्नुहोस्, तपाईंले "Add" देख्नुपर्छ, "Add" चयन गरी प्यारामिटर मानहरू भर्नुहोस्।

  तपाईंले निम्न प्रतिक्रिया देख्नुपर्छ, अर्थात् "add" टुलबाट प्राप्त परिणाम:

  ![Result of running add](../../../../translated_images/ran-tool.a5a6ee878c1369ec1e379b81053395252a441799dbf23416c36ddf288faf8249.ne.png)

बधाई छ, तपाईंले आफ्नो पहिलो सर्भर सफलतापूर्वक सिर्जना र चलाउनुभयो!

### आधिकारिक SDK हरू

MCP ले विभिन्न भाषाहरूका लागि आधिकारिक SDK हरू प्रदान गर्दछ:

- [C# SDK](https://github.com/modelcontextprotocol/csharp-sdk) - Microsoft सँग सहकार्यमा मर्मत गरिएको
- [Java SDK](https://github.com/modelcontextprotocol/java-sdk) - Spring AI सँग सहकार्यमा मर्मत गरिएको
- [TypeScript SDK](https://github.com/modelcontextprotocol/typescript-sdk) - आधिकारिक TypeScript कार्यान्वयन
- [Python SDK](https://github.com/modelcontextprotocol/python-sdk) - आधिकारिक Python कार्यान्वयन
- [Kotlin SDK](https://github.com/modelcontextprotocol/kotlin-sdk) - आधिकारिक Kotlin कार्यान्वयन
- [Swift SDK](https://github.com/modelcontextprotocol/swift-sdk) - Loopwork AI सँग सहकार्यमा मर्मत गरिएको
- [Rust SDK](https://github.com/modelcontextprotocol/rust-sdk) - आधिकारिक Rust कार्यान्वयन

## मुख्य बुँदाहरू

- MCP विकास वातावरण सेटअप भाषा-विशिष्ट SDK हरूको साथ सजिलो छ
- MCP सर्भरहरू निर्माण गर्दा स्पष्ट स्किमासहित टुलहरू सिर्जना र दर्ता गर्नुपर्छ
- विश्वसनीय MCP कार्यान्वयनका लागि परीक्षण र डिबगिङ आवश्यक छ

## नमूनाहरू

- [Java Calculator](../samples/java/calculator/README.md)
- [.Net Calculator](../../../../03-GettingStarted/samples/csharp)
- [JavaScript Calculator](../samples/javascript/README.md)
- [TypeScript Calculator](../samples/typescript/README.md)
- [Python Calculator](../../../../03-GettingStarted/samples/python)

## कार्य

आफ्नो रोजाइको टुल सहित सरल MCP सर्भर सिर्जना गर्नुहोस्:

1. आफ्नो मनपर्ने भाषामा टुल कार्यान्वयन गर्नुहोस् (.NET, Java, Python, वा JavaScript)।
2. इनपुट प्यारामिटरहरू र रिटर्न मानहरू परिभाषित गर्नुहोस्।
3. सर्भरले अपेक्षित रूपमा काम गर्छ कि गर्दैन भनेर सुनिश्चित गर्न inspector टुल चलाउनुहोस्।
4. विभिन्न इनपुटहरूसँग कार्यान्वयन परीक्षण गर्नुहोस्।

## समाधान

[Solution](./solution/README.md)

## थप स्रोतहरू

- [Azure मा Model Context Protocol प्रयोग गरेर एजेन्टहरू निर्माण गर्नुहोस्](https://learn.microsoft.com/azure/developer/ai/intro-agents-mcp)
- [Azure Container Apps सँग Remote MCP (Node.js/TypeScript/JavaScript)](https://learn.microsoft.com/samples/azure-samples/mcp-container-ts/mcp-container-ts/)
- [.NET OpenAI MCP Agent](https://learn.microsoft.com/samples/azure-samples/openai-mcp-agent-dotnet/openai-mcp-agent-dotnet/)

## अब के गर्ने

अर्को: [MCP Clients सँग परिचय](../02-client/README.md)

**अस्वीकरण**:  
यो दस्तावेज AI अनुवाद सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) प्रयोग गरी अनुवाद गरिएको हो। हामी शुद्धताका लागि प्रयासरत छौं, तर कृपया ध्यान दिनुहोस् कि स्वचालित अनुवादमा त्रुटि वा अशुद्धता हुन सक्छ। मूल दस्तावेज यसको मूल भाषामा नै अधिकारिक स्रोत मानिनु पर्छ। महत्वपूर्ण जानकारीका लागि व्यावसायिक मानव अनुवाद सिफारिस गरिन्छ। यस अनुवादको प्रयोगबाट उत्पन्न कुनै पनि गलतफहमी वा गलत व्याख्याका लागि हामी जिम्मेवार छैनौं।