---
sidebar_position: 97
---

# 🟢 اوپن اے آئی پلے گراؤنڈ

<!-- import Playground from '@site/docs/assets/basics/openai_playground.webp'; -->
import Playground from '@site/i18n/ur/docusaurus-plugin-content-docs/current/assets/basics/openai_playground.webp';

<div style={{textAlign: 'center'}}>
    <img src={Playground} className="img-docs" style={{width: "80%"}}/>
</div>
<br/>

:::takeaways
- اوپن اے آئی پلے گراؤنڈ ترتیب دیں۔
- کھیل کے میدان کی بنیادی ترتیب کے بارے میں جانیں۔
:::



اوپن اے آئی ایک اور انٹرفیس فراہم کرتا ہے، ChatGPT ویب سائٹ کے علاوہ، پرامپٹ کرنے کے لیے۔ اسے OpenAI پلے گراؤنڈ کہا جاتا ہے، اور یہ آپ کو ChatGPT پر اور بھی زیادہ کنٹرول فراہم کرتا ہے۔ یہ آپ کو دوسرے AIs تک رسائی کی بھی اجازت دیتا ہے، بشمول ChatGPT، GPT-4 کے مختلف ورژن، اور GPT-3 جیسے پرانے ماڈلز۔

:::note
اوپن اے آئی پلے گراؤنڈ وہ ٹول ہے جسے اس کورس کا مینٹینر اکثر استعمال کرتا ہے۔
:::

## سیٹ اپ ہو جاؤ

- [http://platform.openai.com](http://platform.openai.com) پر جائیں
- سائن ان کریں، اور پرامپٹ کی جانچ شروع کریں!

یا یہ ویڈیو دیکھیں:

<iframe width="560" height="315" src="https://www.youtube.com/embed/6OD14rpokRw" title="YouTube video player" frameBorder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowFullScreen></iframe>

:::note
اس ویڈیو میں ویب سائٹ کا پرانا ورژن دکھایا گیا ہے، لیکن لاگ ان کرنے کا عمل بہت ملتا جلتا ہے۔
:::

## انٹرفیس

پہلے تو یہ انٹرفیس بہت پیچیدہ لگتا ہے۔ بہت سے ڈراپ ڈاؤن اور سلائیڈرز ہیں جو آپ کو ماڈلز کو ترتیب دینے کی اجازت دیتے ہیں۔ ہم اس سبق میں موڈ، سسٹم پرامپٹس، اور ماڈل سلیکشن کا احاطہ کریں گے، اور [اگلے سبق] (https://learnprompting.org/docs/basics/configuration_hyperparameters) میں درجہ حرارت، اوپر P، اور زیادہ سے زیادہ لمبائی جیسی LLM ترتیبات کا احاطہ کریں گے۔

### موڈ

<!-- import Mode from '@site/docs/assets/basics/openai_mode.webp'; -->
import Mode from '@site/i18n/ur/docusaurus-plugin-content-docs/current/assets/basics/openai_mode.webp';

<div className="flex flex-col sm:flex-row justify-between">
  <div>
    صفحہ کے اوپری بائیں جانب 'اسسٹنٹ' ڈراپ ڈاؤن پر کلک کریں۔ یہ ڈراپ ڈاؤن آپ کو اس ماڈل کی قسم کو تبدیل کرنے کی اجازت دیتا ہے جسے آپ استعمال کر رہے ہیں۔ OpenAI کے تین مختلف موڈز ہیں: <code>اسسٹنٹ</code>، <code>Chat</code>، اور <code>مکمل</code>۔ ہم پہلے ہی دو آخری کے بارے میں جان چکے ہیں۔ <code>اسسٹنٹ</code> ماڈلز کا مقصد ڈویلپرز کے API کے استعمال کے لیے ہوتا ہے اور یہ دلچسپ ٹولز استعمال کر سکتے ہیں جیسے کوڈ کو چلانے اور معلومات کی بازیافت کرنا۔ ہم اس کورس میں صرف <code>Chat</code> اور کبھی کبھار <code>مکمل</code> ماڈل استعمال کریں گے۔
  </div>
  <div className="mt-4 sm:mt-0 sm:ml-auto">
    <img src={Mode} className="img-docs w-20 sm:w-auto" />
  </div>
</div>

### سسٹم پرامپٹس

<code>Chat</code> پر سوئچ کرنے کے بعد، پہلی چیز جو آپ کو صفحہ کے بائیں جانب گیٹ اسٹارٹ پاپ اپ کے علاوہ نظر آئے گی وہ ہے SYSTEM ایریا۔ اب تک، ہم نے دو قسم کے پیغامات دیکھے ہیں، USER کے پیغامات، جو صرف وہ پیغامات ہیں جو آپ چیٹ بوٹ کو بھیجتے ہیں، اور اسسٹنٹ پیغامات، جو کہ چیٹ بوٹ کے جوابات ہیں۔ ایک تیسری قسم کا پیغام ہے، سسٹم پرامپٹ، جسے یہ ترتیب دینے کے لیے استعمال کیا جا سکتا ہے کہ AI کیسے جواب دیتا ہے۔

پرائمنگ پرامپٹ لگانے کے لیے یہ بہترین جگہ ہے۔ سسٹم پرامپٹ ہوگا "آپ ایک مددگار معاون ہیں۔" پہلے سے طے شدہ طور پر، لیکن آزمانے کے لیے ایک تفریحی متبادل مثال یہ ہوگی کہ "آپ PirateGPT ہیں۔ ہمیشہ سمندری ڈاکو کی طرح بات کریں۔" مثال [ہمارے پچھلے سبق] سے (https://learnprompting.org/docs/basics/priming_prompt)۔

<!-- import system_prompt from '@site/docs/assets/basics/openai_system_prompt.webp'; -->
import system_prompt from '@site/i18n/ur/docusaurus-plugin-content-docs/current/assets/basics/openai_system_prompt.webp';

<div style={{textAlign: 'center'}}>
    <img src={system_prompt} className="img-docs" style={{width: "80%"}}/>
</div>
<br/>

### ماڈل

<!-- import Model from '@site/docs/assets/basics/openai_model.webp'; -->
import Model from '@site/i18n/ur/docusaurus-plugin-content-docs/current/assets/basics/openai_model.webp';

<div className="flex flex-col sm:flex-row justify-between">
  <div>
  صفحہ کے دائیں جانب ماڈل ڈراپ ڈاؤن پر کلک کریں۔ یہ ڈراپ ڈاؤن آپ کو اس ماڈل کو تبدیل کرنے کی اجازت دیتا ہے جسے آپ استعمال کر رہے ہیں۔ ہر موڈ میں متعدد ماڈلز ہوتے ہیں، لیکن ہم چیٹ والوں پر توجہ مرکوز کریں گے۔ یہ فہرست بہت پیچیدہ معلوم ہوتی ہے (gpt-3.5-turbo کا کیا مطلب ہے؟)، لیکن یہ مختلف ماڈلز کے صرف تکنیکی نام ہیں۔ کوئی بھی چیز جو gpt-3.5-turbo سے شروع ہوتی ہے وہ ChatGPT کا ایک ورژن ہے، جب کہ کوئی بھی چیز جو gpt-4 سے شروع ہوتی ہے وہ GPT-4 کا ورژن ہے، جس نئے ماڈل تک آپ کو ChatGPT Plus سبسکرپشن خریدنے سے رسائی حاصل ہوتی ہے۔

  </div>
  <div className="mt-4 sm:mt-0 sm:ml-auto">
    <img src={Model} className="img-docs w-20 sm:w-auto" />
  </div>
</div>

:::note
ہو سکتا ہے آپ اپنے انٹرفیس میں GPT-4 ورژن نہ دیکھ سکیں۔
:::

ماڈل کے ناموں میں 16K، 32K، یا 128k جیسے نمبر سیاق و سباق کی لمبائی کی نمائندگی کرتے ہیں۔ اگر اس کی وضاحت نہیں کی گئی ہے تو، پہلے سے طے شدہ سیاق و سباق کی لمبائی gpt-3.5 کے لیے 4K اور GPT-4 کے لیے 8k ہے۔ OpenAI باقاعدگی سے ChatGPT (gpt-3.5-turbo) اور GPT-4 دونوں کو اپ ڈیٹ کرتا ہے، اور پرانے ورژن پلیٹ فارم پر محدود مدت کے لیے دستیاب رکھے جاتے ہیں۔ ان پرانے ماڈلز کے نام کے آخر میں اضافی نمبر ہوتے ہیں، جیسے "0613"۔ مثال کے طور پر، ماڈل "gpt-3.5-turbo-16k-0613" 16K سیاق و سباق کی لمبائی کے ساتھ ایک ChatGPT ماڈل ہے، جو 13 جون 2023 کو جاری کیا گیا تھا۔ تاہم، یہ تجویز کیا جاتا ہے کہ ماڈلز کے تازہ ترین ورژن استعمال کریں، جو ایسا نہیں کرتے ہیں۔ کسی بھی تاریخ کی معلومات پر مشتمل ہے۔ ماڈل ورژن کی ایک جامع فہرست [یہاں] (https://platform.openai.com/docs/models/gpt-4) مل سکتی ہے۔

## نتیجہ

اوپن اے آئی پلے گراؤنڈ ایک طاقتور ٹول ہے جو چیٹ جی پی ٹی اور دیگر اے آئی ماڈلز کے ساتھ بات چیت کے لیے زیادہ جدید انٹرفیس فراہم کرتا ہے۔ یہ ترتیب کے اختیارات کی ایک رینج پیش کرتا ہے، بشمول مختلف ماڈلز اور طریقوں کو منتخب کرنے کی صلاحیت۔ ہم باقی ترتیبات کے بارے میں [اگلے سبق] (https://learnprompting.org/docs/basics/configuration_hyperparameters) میں سیکھیں گے۔ پلے گراؤنڈ سسٹم پرامپٹس کو بھی سپورٹ کرتا ہے، جو AI کے جوابات کی رہنمائی کے لیے استعمال کیا جا سکتا ہے۔ اگرچہ انٹرفیس شروع میں پیچیدہ معلوم ہو سکتا ہے، مشق کے ساتھ، یہ OpenAI کے ماڈلز کی صلاحیتوں کو تلاش کرنے کے لیے ایک قیمتی وسیلہ بن جاتا ہے۔ چاہے آپ ChatGPT یا GPT-4 کے تازہ ترین ورژن استعمال کر رہے ہوں، یا پرانے ماڈلز کو تلاش کر رہے ہوں، کھیل کا میدان AI بات چیت اور تجربات کے لیے ایک لچکدار اور مضبوط پلیٹ فارم پیش کرتا ہے۔

جزوی طور پر evintunador نے لکھا ہے۔