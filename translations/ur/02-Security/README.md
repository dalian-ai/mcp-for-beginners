<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "c69f9df7f3215dac8d056020539bac36",
  "translation_date": "2025-07-04T15:53:29+00:00",
  "source_file": "02-Security/README.md",
  "language_code": "ur"
}
-->
# سیکیورٹی کے بہترین طریقے

Model Context Protocol (MCP) کو اپنانا AI پر مبنی ایپلیکیشنز میں طاقتور نئی صلاحیتیں لاتا ہے، لیکن اس کے ساتھ منفرد سیکیورٹی چیلنجز بھی آتے ہیں جو روایتی سافٹ ویئر کے خطرات سے آگے ہیں۔ محفوظ کوڈنگ، کم از کم مراعات، اور سپلائی چین سیکیورٹی جیسے قائم شدہ خدشات کے علاوہ، MCP اور AI کے کاموں کو نئے خطرات کا سامنا ہے جیسے کہ prompt injection، tool poisoning، اور dynamic tool modification۔ اگر ان خطرات کو مناسب طریقے سے نہیں سنبھالا گیا تو یہ ڈیٹا کی چوری، پرائیویسی کی خلاف ورزی، اور غیر متوقع نظامی رویے کا باعث بن سکتے ہیں۔

یہ سبق MCP سے متعلق سب سے اہم سیکیورٹی خطرات کا جائزہ لیتا ہے—جس میں authentication، authorization، ضرورت سے زیادہ اجازتیں، بالواسطہ prompt injection، اور سپلائی چین کی کمزوریاں شامل ہیں—اور ان کو کم کرنے کے لیے عملی کنٹرولز اور بہترین طریقے فراہم کرتا ہے۔ آپ یہ بھی سیکھیں گے کہ Microsoft کے حل جیسے Prompt Shields، Azure Content Safety، اور GitHub Advanced Security کو کیسے استعمال کیا جائے تاکہ آپ کی MCP کی تنصیب مضبوط ہو۔ ان کنٹرولز کو سمجھ کر اور لاگو کر کے، آپ سیکیورٹی کی خلاف ورزی کے امکانات کو نمایاں طور پر کم کر سکتے ہیں اور اپنے AI نظاموں کو مضبوط اور قابل اعتماد بنا سکتے ہیں۔

# سیکھنے کے مقاصد

اس سبق کے اختتام تک، آپ قابل ہوں گے کہ:

- Model Context Protocol (MCP) کی وجہ سے پیدا ہونے والے منفرد سیکیورٹی خطرات کی نشاندہی اور وضاحت کریں، جن میں prompt injection، tool poisoning، ضرورت سے زیادہ اجازتیں، اور سپلائی چین کی کمزوریاں شامل ہیں۔
- MCP سیکیورٹی خطرات کے لیے مؤثر حفاظتی کنٹرولز کو بیان اور لاگو کریں، جیسے مضبوط authentication، کم از کم مراعات، محفوظ ٹوکن مینجمنٹ، اور سپلائی چین کی تصدیق۔
- Microsoft کے حل جیسے Prompt Shields، Azure Content Safety، اور GitHub Advanced Security کو سمجھیں اور استعمال کریں تاکہ MCP اور AI کے کاموں کی حفاظت کی جا سکے۔
- ٹول میٹا ڈیٹا کی تصدیق کی اہمیت کو پہچانیں، dynamic تبدیلیوں کی نگرانی کریں، اور بالواسطہ prompt injection حملوں سے دفاع کریں۔
- قائم شدہ سیکیورٹی بہترین طریقوں—جیسے محفوظ کوڈنگ، سرور کی سختی، اور zero trust architecture—کو اپنی MCP تنصیب میں شامل کریں تاکہ سیکیورٹی خلاف ورزیوں کے امکانات اور اثرات کو کم کیا جا سکے۔

# MCP سیکیورٹی کنٹرولز

کوئی بھی نظام جسے اہم وسائل تک رسائی حاصل ہو، اس کے ساتھ پوشیدہ سیکیورٹی چیلنجز ہوتے ہیں۔ سیکیورٹی کے چیلنجز کو عام طور پر بنیادی سیکیورٹی کنٹرولز اور تصورات کے درست اطلاق کے ذریعے حل کیا جا سکتا ہے۔ چونکہ MCP ابھی نیا متعین کیا گیا ہے، اس لیے اس کی وضاحت تیزی سے بدل رہی ہے اور جیسے جیسے پروٹوکول ترقی کرتا ہے، اس کے اندر سیکیورٹی کنٹرولز بھی بہتر ہوں گے، جو انٹرپرائز اور قائم شدہ سیکیورٹی آرکیٹیکچرز اور بہترین طریقوں کے ساتھ بہتر انضمام کی اجازت دیں گے۔

[Microsoft Digital Defense Report](https://aka.ms/mddr) میں شائع ہونے والی تحقیق کے مطابق، رپورٹ شدہ خلاف ورزیوں میں سے 98% کو مضبوط سیکیورٹی ہائجین کے ذریعے روکا جا سکتا ہے اور کسی بھی قسم کی خلاف ورزی کے خلاف بہترین تحفظ یہ ہے کہ آپ اپنی بنیادی سیکیورٹی ہائجین، محفوظ کوڈنگ کے بہترین طریقے، اور سپلائی چین سیکیورٹی کو درست کریں — وہ آزمودہ طریقے جو ہم پہلے سے جانتے ہیں، سیکیورٹی خطرے کو کم کرنے میں سب سے زیادہ مؤثر ہیں۔

آئیے دیکھتے ہیں کہ MCP کو اپنانے کے دوران آپ سیکیورٹی خطرات کو کیسے حل کرنا شروع کر سکتے ہیں۔

> **Note:** درج ذیل معلومات **29 مئی 2025** تک درست ہیں۔ MCP پروٹوکول مسلسل ترقی کر رہا ہے، اور مستقبل کی تنصیبات میں نئے authentication پیٹرنز اور کنٹرولز شامل ہو سکتے ہیں۔ تازہ ترین اپ ڈیٹس اور رہنمائی کے لیے ہمیشہ [MCP Specification](https://spec.modelcontextprotocol.io/) اور سرکاری [MCP GitHub repository](https://github.com/modelcontextprotocol) اور [security best practice page](https://modelcontextprotocol.io/specification/draft/basic/security_best_practices) کا حوالہ دیں۔

### مسئلہ کا بیان  
اصل MCP وضاحت میں یہ فرض کیا گیا تھا کہ ڈویلپرز اپنا authentication سرور خود لکھیں گے۔ اس کے لیے OAuth اور متعلقہ سیکیورٹی پابندیوں کا علم ضروری تھا۔ MCP سرورز OAuth 2.0 Authorization Servers کے طور پر کام کرتے تھے، جو صارف کی authentication کو براہ راست سنبھالتے تھے بجائے اس کے کہ اسے Microsoft Entra ID جیسے بیرونی سروس کو سونپیں۔ **26 اپریل 2025** سے، MCP وضاحت میں ایک اپ ڈیٹ نے اجازت دی ہے کہ MCP سرورز صارف کی authentication کو بیرونی سروس کو سونپ سکتے ہیں۔

### خطرات
- MCP سرور میں authorization منطق کی غلط ترتیب حساس ڈیٹا کے افشاء اور غلط طریقے سے لاگو کیے گئے رسائی کنٹرولز کا باعث بن سکتی ہے۔
- مقامی MCP سرور پر OAuth ٹوکن کی چوری۔ اگر ٹوکن چوری ہو جائے تو اسے MCP سرور کی نقل کرنے اور اس سروس سے وسائل اور ڈیٹا تک رسائی کے لیے استعمال کیا جا سکتا ہے جس کے لیے OAuth ٹوکن جاری کیا گیا ہے۔

#### Token Passthrough  
authorization وضاحت میں ٹوکن پاس تھرو واضح طور پر ممنوع ہے کیونکہ یہ کئی سیکیورٹی خطرات پیدا کرتا ہے، جن میں شامل ہیں:

#### سیکیورٹی کنٹرولز کی خلاف ورزی  
MCP سرور یا نیچے کی طرف APIs اہم سیکیورٹی کنٹرولز جیسے rate limiting، request validation، یا traffic monitoring نافذ کر سکتے ہیں، جو ٹوکن کے audience یا دیگر اسناد کی پابندیوں پر منحصر ہوتے ہیں۔ اگر کلائنٹس ٹوکنز کو براہ راست نیچے کی طرف APIs کے ساتھ استعمال کر سکیں بغیر MCP سرور کی مناسب تصدیق کے یا یہ یقینی بنائے کہ ٹوکنز صحیح سروس کے لیے جاری کیے گئے ہیں، تو وہ ان کنٹرولز کو نظر انداز کر دیتے ہیں۔

#### جوابدہی اور آڈٹ ٹریل کے مسائل  
جب کلائنٹس اپ اسٹریم جاری کردہ access token کے ساتھ کال کر رہے ہوں جو MCP سرور کے لیے مبہم ہو سکتا ہے، تو MCP سرور MCP کلائنٹس کی شناخت یا تمیز کرنے سے قاصر ہوگا۔  
نیچے کی طرف Resource Server کے لاگز ایسی درخواستیں دکھا سکتے ہیں جو مختلف ماخذ یا شناخت سے آتی ہوئی نظر آئیں، بجائے اس کے کہ وہ MCP سرور ہوں جو اصل میں ٹوکنز کو فارورڈ کر رہا ہے۔  
یہ دونوں عوامل واقعہ کی تحقیقات، کنٹرولز، اور آڈٹنگ کو مشکل بناتے ہیں۔  
اگر MCP سرور ٹوکنز کو ان کے دعووں (مثلاً کردار، مراعات، یا audience) یا دیگر میٹا ڈیٹا کی تصدیق کیے بغیر پاس کرتا ہے، تو چوری شدہ ٹوکن رکھنے والا بدنیت فریق سرور کو ڈیٹا چوری کے لیے پراکسی کے طور پر استعمال کر سکتا ہے۔

#### اعتماد کی حد کے مسائل  
نیچے کی طرف Resource Server مخصوص اداروں کو اعتماد دیتا ہے۔ یہ اعتماد ماخذ یا کلائنٹ کے رویے کے نمونوں کے بارے میں مفروضات شامل کر سکتا ہے۔ اس اعتماد کی حد کو توڑنا غیر متوقع مسائل کا باعث بن سکتا ہے۔  
اگر ٹوکن کو متعدد سروسز بغیر مناسب تصدیق کے قبول کر لیا جائے، تو ایک سروس کے سمجھوتہ ہونے پر حملہ آور اس ٹوکن کو دیگر جڑے ہوئے سروسز تک رسائی کے لیے استعمال کر سکتا ہے۔

#### مستقبل کی مطابقت کا خطرہ  
اگرچہ آج MCP سرور "خالص پراکسی" کے طور پر شروع ہو سکتا ہے، اسے بعد میں سیکیورٹی کنٹرولز شامل کرنے کی ضرورت پڑ سکتی ہے۔ صحیح ٹوکن audience کی علیحدگی سے سیکیورٹی ماڈل کو ترقی دینا آسان ہو جاتا ہے۔

### حفاظتی کنٹرولز

**MCP سرورز کو ایسے کسی بھی ٹوکن کو قبول نہیں کرنا چاہیے جو واضح طور پر MCP سرور کے لیے جاری نہ کیے گئے ہوں**

- **Authorization Logic کا جائزہ لیں اور سخت کریں:** اپنے MCP سرور کی authorization عمل درآمد کا بغور آڈٹ کریں تاکہ صرف مطلوبہ صارفین اور کلائنٹس حساس وسائل تک رسائی حاصل کر سکیں۔ عملی رہنمائی کے لیے دیکھیں [Azure API Management Your Auth Gateway For MCP Servers | Microsoft Community Hub](https://techcommunity.microsoft.com/blog/integrationsonazureblog/azure-api-management-your-auth-gateway-for-mcp-servers/4402690) اور [Using Microsoft Entra ID To Authenticate With MCP Servers Via Sessions - Den Delimarsky](https://den.dev/blog/mcp-server-auth-entra-id-session/)۔  
- **محفوظ ٹوکن کے طریقے نافذ کریں:** [Microsoft کے ٹوکن کی تصدیق اور مدت کے بہترین طریقے](https://learn.microsoft.com/en-us/entra/identity-platform/access-tokens) پر عمل کریں تاکہ access tokens کے غلط استعمال اور ٹوکن کی دوبارہ بازی یا چوری کے خطرے کو کم کیا جا سکے۔  
- **ٹوکن اسٹوریج کی حفاظت کریں:** ہمیشہ ٹوکنز کو محفوظ طریقے سے ذخیرہ کریں اور انہیں آرام اور منتقلی کے دوران انکرپٹ کریں۔ عمل درآمد کے نکات کے لیے دیکھیں [Use secure token storage and encrypt tokens](https://youtu.be/uRdX37EcCwg?si=6fSChs1G4glwXRy2)۔

# MCP سرورز کے لیے ضرورت سے زیادہ اجازتیں

### مسئلہ کا بیان  
MCP سرورز کو اس سروس/وسائل کے لیے ضرورت سے زیادہ اجازتیں دی گئی ہو سکتی ہیں جس تک وہ رسائی حاصل کر رہے ہیں۔ مثال کے طور پر، ایک MCP سرور جو AI سیلز ایپلیکیشن کا حصہ ہے اور انٹرپرائز ڈیٹا اسٹور سے جڑ رہا ہے، اسے صرف سیلز ڈیٹا تک محدود رسائی ہونی چاہیے، نہ کہ اسٹور کی تمام فائلوں تک۔ کم از کم مراعات کے اصول (جو سب سے پرانا سیکیورٹی اصول ہے) کے مطابق، کسی بھی وسائل کو اس سے زیادہ اجازت نہیں دی جانی چاہیے جتنا کہ اسے اپنے کام انجام دینے کے لیے درکار ہو۔ AI اس معاملے میں ایک چیلنج پیش کرتا ہے کیونکہ اسے لچکدار بنانے کے لیے، صحیح اجازتوں کی تعریف کرنا مشکل ہو سکتا ہے۔

### خطرات  
- ضرورت سے زیادہ اجازتیں دینے سے وہ ڈیٹا چوری یا ترمیم ہو سکتی ہے جس تک MCP سرور کو رسائی نہیں دی گئی تھی۔ اگر ڈیٹا ذاتی شناختی معلومات (PII) ہو تو یہ پرائیویسی کا مسئلہ بھی بن سکتا ہے۔

### حفاظتی کنٹرولز  
- **کم از کم مراعات کا اصول اپنائیں:** MCP سرور کو صرف وہی کم از کم اجازتیں دیں جو اس کے کام انجام دینے کے لیے ضروری ہوں۔ ان اجازتوں کا باقاعدہ جائزہ لیں اور اپ ڈیٹ کریں تاکہ یہ یقینی بنایا جا سکے کہ وہ ضرورت سے زیادہ نہ ہوں۔ تفصیلی رہنمائی کے لیے دیکھیں [Secure least-privileged access](https://learn.microsoft.com/entra/identity-platform/secure-least-privileged-access)۔  
- **Role-Based Access Control (RBAC) استعمال کریں:** MCP سرور کو مخصوص وسائل اور کارروائیوں کے لیے محدود کردہ کردار تفویض کریں، وسیع یا غیر ضروری اجازتوں سے گریز کریں۔  
- **اجازتوں کی نگرانی اور آڈٹ کریں:** اجازتوں کے استعمال کی مسلسل نگرانی کریں اور رسائی کے لاگز کا آڈٹ کریں تاکہ ضرورت سے زیادہ یا غیر استعمال شدہ مراعات کو فوری طور پر شناخت اور درست کیا جا سکے۔

# بالواسطہ prompt injection حملے

### مسئلہ کا بیان

بدنیت یا سمجھوتہ شدہ MCP سرورز اہم خطرات پیدا کر سکتے ہیں، جیسے صارف کے ڈیٹا کا افشاء یا غیر ارادی کارروائیوں کی اجازت دینا۔ یہ خطرات خاص طور پر AI اور MCP پر مبنی کاموں میں اہم ہیں، جہاں:

- **Prompt Injection حملے:** حملہ آور prompts یا بیرونی مواد میں بدنیت ہدایات شامل کرتے ہیں، جس سے AI نظام غیر ارادی کارروائیاں کرتا ہے یا حساس ڈیٹا لیک ہو جاتا ہے۔ مزید جانیں: [Prompt Injection](https://simonwillison.net/2025/Apr/9/mcp-prompt-injection/)  
- **Tool Poisoning:** حملہ آور ٹول میٹا ڈیٹا (جیسے وضاحتیں یا پیرامیٹرز) میں چالاکی سے تبدیلی کرتے ہیں تاکہ AI کے رویے کو متاثر کیا جا سکے، ممکنہ طور پر سیکیورٹی کنٹرولز کو بائی پاس کیا جا سکے یا ڈیٹا چوری کی جا سکے۔ تفصیلات: [Tool Poisoning](https://invariantlabs.ai/blog/mcp-security-notification-tool-poisoning-attacks)  
- **Cross-Domain Prompt Injection:** بدنیت ہدایات دستاویزات، ویب صفحات، یا ای میلز میں شامل کی جاتی ہیں، جنہیں AI پروسیس کرتا ہے، جس سے ڈیٹا لیک یا چالاکی ہوتی ہے۔  
- **Dynamic Tool Modification (Rug Pulls):** صارف کی منظوری کے بعد ٹول کی تعریفیں تبدیل کی جا سکتی ہیں، جس سے نئے بدنیت رویے بغیر صارف کی آگاہی کے متعارف ہوتے ہیں۔

یہ کمزوریاں MCP سرورز اور ٹولز کو آپ کے ماحول میں شامل کرتے وقت مضبوط تصدیق، نگرانی، اور سیکیورٹی کنٹرولز کی ضرورت کو اجاگر کرتی ہیں۔ مزید تفصیل کے لیے اوپر دیے گئے لنکس دیکھیں۔

![prompt-injection-lg-2048x1034](../../../translated_images/prompt-injection.ed9fbfde297ca877c15bc6daa808681cd3c3dc7bf27bbbda342ef1ba5fc4f52d.ur.png)

**بالواسطہ Prompt Injection** (جسے cross-domain prompt injection یا XPIA بھی کہا جاتا ہے) جنریٹو AI نظاموں میں ایک سنگین کمزوری ہے، بشمول وہ جو Model Context Protocol (MCP) استعمال کرتے ہیں۔ اس حملے میں، بدنیت ہدایات بیرونی مواد—جیسے دستاویزات، ویب صفحات، یا ای میلز—میں چھپی ہوتی ہیں۔ جب AI نظام اس مواد کو پروسیس کرتا ہے، تو یہ چھپی ہوئی ہدایات کو جائز صارف کے احکامات سمجھ کر غیر ارادی کارروائیاں کر سکتا ہے، جیسے ڈیٹا لیک، نقصان دہ مواد کی تخلیق، یا صارف کے تعاملات میں چالاکی۔ تفصیلی وضاحت اور حقیقی دنیا کی مثالوں کے لیے دیکھیں [Prompt Injection](https://simonwillison.net/2025/Apr/9/mcp-prompt-injection/)۔

اس حملے کی ایک خاص طور پر خطرناک شکل **Tool Poisoning** ہے۔ یہاں، حملہ آور MCP ٹولز کے میٹا ڈیٹا (جیسے ٹول کی وضاحتیں یا پیرامیٹرز) میں بدنیت ہدایات شامل کرتے ہیں۔ چونکہ بڑے زبان کے ماڈلز (LLMs) اس میٹا ڈیٹا پر انحصار کرتے ہیں کہ وہ کون سے ٹولز کو کال کریں، اس لیے خراب شدہ وضاحتیں ماڈل کو غیر مجاز ٹول کالز کرنے یا سیکیورٹی کنٹرولز کو بائی پاس کرنے پر مجبور کر سکتی ہیں۔ یہ چالاکیاں اکثر صارفین کے لیے نظر نہیں آتیں لیکن AI نظام انہیں سمجھ کر عمل کرتا ہے۔ یہ خطرہ خاص طور پر ہوسٹ کیے گئے MCP سرور ماحول میں بڑھ جاتا ہے، جہاں صارف کی منظوری کے بعد ٹول کی تعریفیں اپ ڈیٹ کی جا سکتی ہیں—جسے کبھی کبھار "[rug pull](https://www.wiz.io/blog/mcp-security-research-briefing#remote-servers-22)" کہا جاتا ہے۔ ایسے معاملات میں، ایک ٹول جو پہلے محفوظ تھا، بعد میں بدنیت کارروائیاں کرنے کے لیے تبدیل کیا جا سکتا ہے، جیسے ڈیٹا چوری یا نظامی رویے میں تبدیلی، بغیر صارف کی اطلاع کے۔ اس حملے کے بارے میں مزید جاننے کے لیے دیکھیں [Tool Poisoning](https://invariantlabs.ai/blog/mcp-security-notification-tool-poisoning-attacks)۔

![tool-injection-lg-2048x1239 (1)](../../../translated_images/tool-injection.3b0b4a6b24de6befe7d3afdeae44138ef005881aebcfc84c6f61369ce31e3640.ur.png)

## خطرات  
غیر ارادی AI کارروائیاں مختلف سیکیورٹی خطرات پیش کرتی ہیں جن میں ڈیٹا چوری اور پرائیویسی کی خلاف ورزیاں شامل ہیں۔

### حفاظتی کنٹرولز  
### Indirect Prompt Injection حملوں سے بچاؤ کے لیے prompt shields کا استعمال  
-----------------------------------------------------------------------------

**AI Prompt Shields** Microsoft کی طرف سے تیار کردہ ایک حل ہے جو براہ راست اور بالواسطہ prompt injection حملوں سے دفاع کرتا ہے۔ یہ درج ذیل طریقوں سے مدد کرتے ہیں:

1.  **پہچان اور فلٹرنگ:** Prompt Shields جدید مشین لرننگ الگورتھمز اور قدرتی زبان کی پروسیسنگ استعمال کرتے ہیں تاکہ بیرونی مواد جیسے دستاویزات، ویب صفحات، یا ای میلز میں شامل بدنیت ہدایات کو پہچانا اور فلٹر کیا جا سکے۔  
2.  **Spotlighting:** یہ تکنیک AI نظام کو جائز نظامی ہدایات اور ممکنہ غیر معتبر بیرونی ان پٹس کے درمیان فرق کرنے میں مدد دیتی ہے۔ ان پٹ ٹیکسٹ کو اس طرح تبدیل کر کے جو ماڈل کے لیے زیادہ متعلقہ ہو، Spotlighting یقینی بناتا ہے کہ AI بدنیت ہدایات کو بہتر طور پر پہچان کر نظر انداز کر سکے۔  
3.  **Delimiters اور Datamarking:** سسٹم میسج میں delimiters شامل کرنا واضح طور پر ان پٹ ٹیکسٹ کی جگہ بتاتا ہے، جس سے AI نظام صارف کے ان پٹس کو ممکنہ نقصان دہ بیرونی مواد سے الگ کر سکتا ہے۔ Datamarking اس تصور کو آگے بڑھاتا ہے خاص مارکرز کے ذریعے قابل اعتماد اور غیر قابل اعتماد ڈیٹا کی حد بندی کو نمایاں کر کے۔  
4.  **مسلسل نگرانی اور اپ ڈیٹس:** Microsoft مسلسل Prompt Shields کی نگرانی اور اپ ڈیٹ کرتا ہے تاکہ نئے اور بدلتے ہوئے خطرات کا مقابلہ کیا جا سکے۔ یہ پیشگی حکمت عملی دفاع کو
سپلائی چین سیکیورٹی AI کے دور میں بنیادی حیثیت رکھتی ہے، لیکن آپ کی سپلائی چین کی تعریف کا دائرہ وسیع ہو چکا ہے۔ روایتی کوڈ پیکجز کے علاوہ، اب آپ کو تمام AI سے متعلقہ اجزاء، بشمول foundation models، embeddings services، context providers، اور third-party APIs کی سختی سے تصدیق اور نگرانی کرنی ہوگی۔ اگر ان میں مناسب انتظام نہ کیا جائے تو ہر ایک میں کمزوریاں یا خطرات پیدا ہو سکتے ہیں۔

**AI اور MCP کے لیے کلیدی سپلائی چین سیکیورٹی کے طریقے:**
- **انضمام سے پہلے تمام اجزاء کی تصدیق کریں:** اس میں صرف اوپن سورس لائبریریز ہی نہیں بلکہ AI ماڈلز، ڈیٹا ذرائع، اور بیرونی APIs بھی شامل ہیں۔ ہمیشہ ماخذ، لائسنسنگ، اور معروف کمزوریوں کی جانچ کریں۔
- **محفوظ تعیناتی کے عمل کو برقرار رکھیں:** خودکار CI/CD پائپ لائنز استعمال کریں جن میں سیکیورٹی اسکیننگ شامل ہو تاکہ مسائل جلدی پکڑے جا سکیں۔ یقینی بنائیں کہ صرف قابل اعتماد آرٹیفیکٹس پروڈکشن میں تعینات ہوں۔
- **مسلسل نگرانی اور آڈٹ کریں:** تمام انحصار، بشمول ماڈلز اور ڈیٹا سروسز، کی جاری نگرانی نافذ کریں تاکہ نئی کمزوریاں یا سپلائی چین حملے معلوم ہو سکیں۔
- **کم از کم مراعات اور رسائی کنٹرولز لاگو کریں:** ماڈلز، ڈیٹا، اور سروسز تک رسائی صرف اتنی محدود رکھیں جتنی آپ کے MCP سرور کے کام کے لیے ضروری ہو۔
- **خطرات کا فوری جواب دیں:** متاثرہ اجزاء کی پیچنگ یا تبدیلی کے لیے ایک عمل رکھیں، اور اگر کوئی خلاف ورزی ہو تو راز یا اسناد کو تبدیل کریں۔

[GitHub Advanced Security](https://github.com/security/advanced-security) جیسی خصوصیات فراہم کرتا ہے جیسے کہ secret scanning، dependency scanning، اور CodeQL تجزیہ۔ یہ ٹولز [Azure DevOps](https://azure.microsoft.com/en-us/products/devops) اور [Azure Repos](https://azure.microsoft.com/en-us/products/devops/repos/) کے ساتھ مربوط ہوتے ہیں تاکہ ٹیموں کو کوڈ اور AI سپلائی چین کے اجزاء میں کمزوریوں کی شناخت اور ان کا سدباب کرنے میں مدد ملے۔

مائیکروسافٹ بھی تمام مصنوعات کے لیے اندرونی طور پر وسیع سپلائی چین سیکیورٹی طریقے نافذ کرتا ہے۔ مزید جاننے کے لیے [The Journey to Secure the Software Supply Chain at Microsoft](https://devblogs.microsoft.com/engineering-at-microsoft/the-journey-to-secure-the-software-supply-chain-at-microsoft/) ملاحظہ کریں۔


# قائم شدہ سیکیورٹی بہترین طریقے جو آپ کی MCP نفاذ کی سیکیورٹی کو بہتر بنائیں گے

کوئی بھی MCP نفاذ آپ کی تنظیم کے ماحول کی موجودہ سیکیورٹی حالت کو وراثت میں لیتا ہے جس پر یہ بنایا گیا ہے، لہٰذا جب آپ MCP کو اپنے مجموعی AI نظام کے ایک جزو کے طور پر دیکھیں تو یہ تجویز کیا جاتا ہے کہ آپ اپنی موجودہ سیکیورٹی حالت کو بہتر بنانے پر غور کریں۔ درج ذیل قائم شدہ سیکیورٹی کنٹرول خاص طور پر متعلقہ ہیں:

- آپ کی AI ایپلیکیشن میں محفوظ کوڈنگ کے بہترین طریقے — [OWASP Top 10](https://owasp.org/www-project-top-ten/)، [OWASP Top 10 for LLMs](https://genai.owasp.org/download/43299/?tmstv=1731900559) کے خلاف تحفظ، راز اور ٹوکنز کے لیے محفوظ والٹس کا استعمال، تمام ایپلیکیشن اجزاء کے درمیان اینڈ ٹو اینڈ محفوظ مواصلات کا نفاذ، وغیرہ۔
- سرور کی سختی — جہاں ممکن ہو MFA کا استعمال کریں، پیچز کو اپ ٹو ڈیٹ رکھیں، رسائی کے لیے سرور کو تھرڈ پارٹی شناخت فراہم کنندہ کے ساتھ مربوط کریں، وغیرہ۔
- ڈیوائسز، انفراسٹرکچر، اور ایپلیکیشنز کو پیچز کے ساتھ اپ ٹو ڈیٹ رکھیں۔
- سیکیورٹی مانیٹرنگ — AI ایپلیکیشن (بشمول MCP کلائنٹ/سرورز) کی لاگنگ اور نگرانی کا نفاذ اور ان لاگز کو مرکزی SIEM کو بھیجنا تاکہ غیر معمولی سرگرمیوں کا پتہ چلایا جا سکے۔
- زیرو ٹرسٹ آرکیٹیکچر — نیٹ ورک اور شناختی کنٹرولز کے ذریعے اجزاء کو منطقی طور پر الگ کرنا تاکہ اگر AI ایپلیکیشن متاثر ہو جائے تو افقی حرکت کو کم سے کم کیا جا سکے۔

# اہم نکات

- سیکیورٹی کے بنیادی اصول اب بھی انتہائی اہم ہیں: محفوظ کوڈنگ، کم از کم مراعات، سپلائی چین کی تصدیق، اور مسلسل نگرانی MCP اور AI ورک لوڈز کے لیے ضروری ہیں۔
- MCP نئے خطرات متعارف کراتا ہے—جیسے prompt injection، tool poisoning، اور ضرورت سے زیادہ اجازتیں—جن کے لیے روایتی اور AI مخصوص کنٹرولز دونوں کی ضرورت ہے۔
- مضبوط توثیق، اجازت، اور ٹوکن مینجمنٹ کے طریقے استعمال کریں، جہاں ممکن ہو Microsoft Entra ID جیسے بیرونی شناخت فراہم کنندگان کا فائدہ اٹھائیں۔
- بالواسطہ prompt injection اور tool poisoning سے بچاؤ کے لیے ٹول میٹا ڈیٹا کی تصدیق کریں، متحرک تبدیلیوں کی نگرانی کریں، اور Microsoft Prompt Shields جیسے حل استعمال کریں۔
- اپنی AI سپلائی چین کے تمام اجزاء—بشمول ماڈلز، embeddings، اور context providers—کو کوڈ انحصار کی طرح ہی سختی سے سنبھالیں۔
- MCP کی بدلتی ہوئی وضاحتوں کے ساتھ اپ ٹو ڈیٹ رہیں اور کمیونٹی میں حصہ لے کر محفوظ معیارات کی تشکیل میں مدد کریں۔

# اضافی وسائل

- [Microsoft Digital Defense Report](https://aka.ms/mddr)
- [MCP Specification](https://spec.modelcontextprotocol.io/)
- [Prompt Injection in MCP (Simon Willison)](https://simonwillison.net/2025/Apr/9/mcp-prompt-injection/)
- [Tool Poisoning Attacks (Invariant Labs)](https://invariantlabs.ai/blog/mcp-security-notification-tool-poisoning-attacks)
- [Rug Pulls in MCP (Wiz Security)](https://www.wiz.io/blog/mcp-security-research-briefing#remote-servers-22)
- [Prompt Shields Documentation (Microsoft)](https://learn.microsoft.com/azure/ai-services/content-safety/concepts/jailbreak-detection)
- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [OWASP Top 10 for LLMs](https://genai.owasp.org/download/43299/?tmstv=1731900559)
- [GitHub Advanced Security](https://github.com/security/advanced-security)
- [Azure DevOps](https://azure.microsoft.com/products/devops)
- [Azure Repos](https://azure.microsoft.com/products/devops/repos/)
- [The Journey to Secure the Software Supply Chain at Microsoft](https://devblogs.microsoft.com/engineering-at-microsoft/the-journey-to-secure-the-software-supply-chain-at-microsoft/)
- [Secure Least-Privileged Access (Microsoft)](https://learn.microsoft.com/entra/identity-platform/secure-least-privileged-access)
- [Best Practices for Token Validation and Lifetime](https://learn.microsoft.com/entra/identity-platform/access-tokens)
- [Use Secure Token Storage and Encrypt Tokens (YouTube)](https://youtu.be/uRdX37EcCwg?si=6fSChs1G4glwXRy2)
- [Azure API Management as Auth Gateway for MCP](https://techcommunity.microsoft.com/blog/integrationsonazureblog/azure-api-management-your-auth-gateway-for-mcp-servers/4402690)
- [MCP Security Best Practice](https://modelcontextprotocol.io/specification/draft/basic/security_best_practices)
- [Using Microsoft Entra ID to Authenticate with MCP Servers](https://den.dev/blog/mcp-server-auth-entra-id-session/)

### اگلا

اگلا: [Chapter 3: Getting Started](../03-GettingStarted/README.md)

**دستخطی دستبرداری**:  
یہ دستاویز AI ترجمہ سروس [Co-op Translator](https://github.com/Azure/co-op-translator) کے ذریعے ترجمہ کی گئی ہے۔ اگرچہ ہم درستگی کے لیے کوشاں ہیں، براہ کرم آگاہ رہیں کہ خودکار ترجمے میں غلطیاں یا عدم درستیاں ہو سکتی ہیں۔ اصل دستاویز اپنی مادری زبان میں ہی معتبر ماخذ سمجھی جانی چاہیے۔ اہم معلومات کے لیے پیشہ ور انسانی ترجمہ کی سفارش کی جاتی ہے۔ اس ترجمے کے استعمال سے پیدا ہونے والی کسی بھی غلط فہمی یا غلط تشریح کی ذمہ داری ہم پر عائد نہیں ہوتی۔