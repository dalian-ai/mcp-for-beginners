<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "d0f0d7012325b286e4a717791b23ae7e",
  "translation_date": "2025-07-09T23:18:07+00:00",
  "source_file": "03-GettingStarted/01-first-server/solution/python/README.md",
  "language_code": "my"
}
-->
# ဒီနမူနာကို chạyခြင်း

`uv` ကို 설치ဖို့ အကြံပြုထားပေမယ့် မလိုအပ်ပါ၊ [ညွှန်ကြားချက်များ](https://docs.astral.sh/uv/#highlights) ကိုကြည့်ပါ။

## -0- virtual environment တစ်ခု ဖန်တီးခြင်း

```bash
python -m venv venv
```

## -1- virtual environment ကို ဖွင့်ခြင်း

```bash
venv\Scrips\activate
```

## -2- လိုအပ်သော dependencies များ 설치ခြင်း

```bash
pip install "mcp[cli]"
```

## -3- နမူနာကို chạyခြင်း

```bash
mcp run server.py
```

## -4- နမူနာကို စမ်းသပ်ခြင်း

server ကို terminal တစ်ခုမှာ chạyထားပြီးနောက်၊ terminal တစ်ခုကို ထပ်ဖွင့်ပြီး အောက်ပါ command ကို chạyပါ။

```bash
mcp dev server.py
```

ဒါက web server တစ်ခုကို visual interface နဲ့ စတင်ပေးမှာဖြစ်ပြီး နမူနာကို စမ်းသပ်နိုင်ပါလိမ့်မယ်။

server ချိတ်ဆက်ပြီးနောက် -

- tools များကို စာရင်းပြပြီး `add` ကို args 2 နဲ့ 4 ဖြင့် chạyကြည့်ပါ၊ ရလဒ်မှာ 6 ကိုမြင်ရပါမယ်။

- resources နဲ့ resource template ကိုသွားပြီး get_greeting ကိုခေါ်ပါ၊ နာမည်တစ်ခုရိုက်ထည့်လိုက်ရင် သင့်ရဲ့နာမည်နဲ့ မင်္ဂလာပါဆိုတဲ့စာကိုမြင်ရပါလိမ့်မယ်။

### CLI mode မှာ စမ်းသပ်ခြင်း

သင် chạyထားတဲ့ inspector က Node.js app တစ်ခုဖြစ်ပြီး `mcp dev` က အဲဒီ app ကို wrapper လုပ်ထားတာပါ။

အောက်ပါ command ကို chạyခြင်းဖြင့် CLI mode မှာ တိုက်ရိုက် စတင်နိုင်ပါတယ်။

```bash
npx @modelcontextprotocol/inspector --cli mcp run server.py --method tools/list
```

ဒါက server မှာ ရနိုင်တဲ့ tools အားလုံးကို စာရင်းပြပါလိမ့်မယ်။ အောက်ပါ output ကိုမြင်ရပါမယ်။

```text
{
  "tools": [
    {
      "name": "add",
      "description": "Add two numbers",
      "inputSchema": {
        "type": "object",
        "properties": {
          "a": {
            "title": "A",
            "type": "integer"
          },
          "b": {
            "title": "B",
            "type": "integer"
          }
        },
        "required": [
          "a",
          "b"
        ],
        "title": "addArguments"
      }
    }
  ]
}
```

tool တစ်ခုကို ခေါ်ရန် -

```bash
npx @modelcontextprotocol/inspector --cli mcp run server.py --method tools/call --tool-name add --tool-arg a=1 --tool-arg b=2
```

အောက်ပါ output ကိုမြင်ရပါလိမ့်မယ်။

```text
{
  "content": [
    {
      "type": "text",
      "text": "3"
    }
  ],
  "isError": false
}
```

> ![!TIP]
> inspector ကို browser မှာ chạyတာထက် CLI mode မှာ chạyတာ ပိုမြန်တတ်ပါတယ်။
> inspector အကြောင်း ပိုမိုသိရှိရန် [ဒီမှာ](https://github.com/modelcontextprotocol/inspector) ဖတ်ပါ။

**အကြောင်းကြားချက်**  
ဤစာတမ်းကို AI ဘာသာပြန်ဝန်ဆောင်မှု [Co-op Translator](https://github.com/Azure/co-op-translator) ဖြင့် ဘာသာပြန်ထားပါသည်။ ကျွန်ုပ်တို့သည် တိကျမှန်ကန်မှုအတွက် ကြိုးစားသော်လည်း အလိုအလျောက် ဘာသာပြန်ခြင်းတွင် အမှားများ သို့မဟုတ် မှားယွင်းမှုများ ပါဝင်နိုင်ကြောင်း သတိပြုပါရန် မေတ္တာရပ်ခံအပ်ပါသည်။ မူရင်းစာတမ်းကို မိမိဘာသာစကားဖြင့်သာ တရားဝင်အချက်အလက်အဖြစ် ယူဆသင့်ပါသည်။ အရေးကြီးသော အချက်အလက်များအတွက် လူ့ဘာသာပြန်ပညာရှင်မှ ဘာသာပြန်ခြင်းကို အကြံပြုပါသည်။ ဤဘာသာပြန်ချက်ကို အသုံးပြုရာမှ ဖြစ်ပေါ်လာနိုင်သည့် နားလည်မှုမှားယွင်းမှုများအတွက် ကျွန်ုပ်တို့သည် တာဝန်မယူပါ။