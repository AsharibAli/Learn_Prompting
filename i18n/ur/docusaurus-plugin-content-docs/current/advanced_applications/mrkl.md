---
sidebar_position: 2
---

# 🟡 LLMs ٹولز کا استعمال کرتے ہوئے

MRKL سسٹمز (@karpas2022mrkl) (ماڈیولر ریزننگ، نالج اینڈ لینگویج، جس کا اعلان "معجزہ" ہے)
ایک **نیورو علامتی فن تعمیر** ہیں جو LLMs (عصبی حساب کتاب) اور بیرونی
پیچیدہ مسائل کو حل کرنے کے لیے ٹولز جیسے کیلکولیٹر (علامتی حساب کتاب)۔

ایک MRKL سسٹم ماڈیولز کے ایک سیٹ پر مشتمل ہوتا ہے (مثال کے طور پر ایک کیلکولیٹر، موسم کا API، ڈیٹا بیس، وغیرہ) اور ایک روٹر جو فیصلہ کرتا ہے کہ آنے والی قدرتی زبان کے سوالات کو مناسب ماڈیول تک کیسے 'روٹ' کرنا ہے۔

MRKL سسٹم کی ایک سادہ مثال LLM ہے جو کر سکتا ہے۔
کیلکولیٹر ایپ استعمال کریں۔ یہ ایک واحد ماڈیول سسٹم ہے، جہاں ایل ایل ایم روٹر ہے۔
جب پوچھا گیا، ''100*100 کیا ہے؟''، ایل ایل ایم اس کا انتخاب کر سکتا ہے۔
پرامپٹ سے نمبر نکالیں، اور پھر MRKL سسٹم کو کیلکولیٹر استعمال کرنے کو کہیں۔
نتیجہ کا حساب لگانے کے لیے ایپ۔ یہ مندرجہ ذیل کی طرح نظر آسکتا ہے:

<pre>
<p>100*100 کیا ہے؟</p>

<span className="bluegreen-highlight">کیلکولیٹر[100*100]</span>
</pre>

MRKL سسٹم لفظ `CALCULATOR` دیکھے گا اور `100*100` کو کیلکولیٹر ایپ میں پلگ کرے گا۔
اس سادہ خیال کو آسانی سے مختلف علامتی کمپیوٹنگ ٹولز تک بڑھایا جا سکتا ہے۔

ایپلی کیشنز کی درج ذیل اضافی مثالوں پر غور کریں:

- ایک چیٹ بوٹ جو مالیاتی ڈیٹا بیس کے بارے میں سوالات کا جواب دینے کے قابل ہے۔
صارف کے ٹیکسٹ سے SQL استفسار بنانے کے لیے معلومات نکالنا۔

<pre>
<p>اس وقت Apple کے اسٹاک کی قیمت کیا ہے؟</p>

<span className="bluegreen-highlight">موجودہ قیمت ڈیٹا بیس ہے[SELECT price FROM stock WHERE company = "Apple" AND time = "now"]۔</span>
</pre>

- ایک چیٹ بوٹ جو نکال کر موسم کے بارے میں سوالات کا جواب دینے کے قابل ہے۔
پرامپٹ سے معلومات حاصل کریں اور معلومات کو بازیافت کرنے کے لیے موسم کا API استعمال کریں۔

<pre>
<p>نیو یارک میں موسم کیسا ہے؟</p>

<span className="bluegreen-highlight">موسم WEATHER_API[نیویارک] ہے۔</span>
</pre>

- یا اس سے بھی زیادہ پیچیدہ کام جو متعدد ڈیٹا ذرائع پر منحصر ہوتے ہیں، جیسے کہ
درج ذیل:


import mrkl_task from '@site/docs/assets/advanced/mrkl_task.webp';
import dataset from '@site/docs/assets/advanced/mrkl/dataset.webp';
import load_dataset from '@site/docs/assets/advanced/mrkl/load_dataset.webp';
import model from '@site/docs/assets/advanced/mrkl/model.webp';
import extract from '@site/docs/assets/advanced/mrkl/extract.webp';
import search from '@site/docs/assets/advanced/mrkl/search.webp';
import final from '@site/docs/assets/advanced/mrkl/final.webp';

<div style={{textAlign: 'center'}}>
   <img src={mrkl_task} اسٹائل={{چوڑائی: "500px"}}/>
</div>

<div style={{textAlign: 'center'}}>
مثال MRKL سسٹم (AI21)
</div>


## ایک مثال

میں نے Dust.tt کا استعمال کرتے ہوئے اصل کاغذ سے ایک مثال MRKL سسٹم کو دوبارہ پیش کیا ہے،
لنک کردہ [یہاں](https://dust.tt/w/ddebdfcdde/a/98bdd65cb7)۔
سسٹم ریاضی کا مسئلہ پڑھتا ہے (جیسے `20 گنا 5^6 کیا ہے؟`)، اعداد اور کارروائیاں نکالتا ہے،
اور انہیں کیلکولیٹر ایپ کے لیے ریفارمیٹ کرتا ہے (جیسے `20*5^6`)۔ یہ پھر فارمیٹ شدہ مساوات بھیجتا ہے۔
Google کی کیلکولیٹر ایپ پر، اور نتیجہ واپس کرتا ہے۔ نوٹ کریں کہ اصل کاغذ راؤٹر (ایل ایل ایم) پر پرامپٹ ٹیوننگ کرتا ہے، لیکن میں اس مثال میں نہیں کرتا۔ آئیے دیکھتے ہیں کہ یہ کیسے کام کرتا ہے:

سب سے پہلے، میں نے Dust `Datasets` ٹیب میں ایک سادہ ڈیٹا سیٹ بنایا۔


<div style={{textAlign: 'center'}}>
   <LazyLoadImage src={dataset} style={{width: "750px"}} />
</div>

پھر، میں نے 'Specification' ٹیب پر سوئچ کیا اور ایک 'ان پٹ' بلاک کا استعمال کرتے ہوئے ڈیٹاسیٹ کو لوڈ کیا۔

<div style={{textAlign: 'center'}}>
   <LazyLoadImage src={load_dataset} style={{width: "750px"}} />
</div>

اگلا، میں نے ایک `llm` بلاک بنایا جو نمبرز اور آپریشنز کو نکالتا ہے۔ نوٹ کریں کہ کیسے
پرامپٹ میں میں نے اسے بتایا کہ ہم گوگل کا کیلکولیٹر استعمال کریں گے۔ میں جو ماڈل استعمال کرتا ہوں (GPT-3)
ممکنہ طور پر گوگل کے کیلکولیٹر کے بارے میں پہلے سے تربیت کے بارے میں کچھ علم ہے۔

<div style={{textAlign: 'center'}}>
   <LazyLoadImage src={model} style={{width: "750px"}} />
</div>

پھر، میں نے ایک `کوڈ` بلاک بنایا، جو ہٹانے کے لیے کچھ آسان جاوا اسکرپٹ کوڈ چلاتا ہے۔
تکمیل سے خالی جگہیں.

<div style={{textAlign: 'center'}}>
   <LazyLoadImage src={extract} style={{width: "750px"}} />
</div>

آخر میں، میں نے ایک 'تلاش' بلاک بنایا جو گوگل کے کیلکولیٹر کو دوبارہ فارمیٹ شدہ مساوات بھیجتا ہے۔

<div style={{textAlign: 'center'}}>
   <LazyLoadImage src={search} style={{width: "750px"}} />
</div>

ذیل میں ہم حتمی نتائج دیکھ سکتے ہیں، جو سب درست ہیں!

<div style={{textAlign: 'center'}}>
   <LazyLoadImage src={final} style={{width: "750px"}} />
</div>

[یہاں] (https://dust.tt/w/ddebdfcdde/a/98bdd65cb7) اس کھیل کے میدان کے ساتھ کلون اور تجربہ کرنے کے لیے آزاد محسوس کریں۔

## نوٹس
MRKL کو [AI21](https://www.ai21.com/) نے تیار کیا اور اصل میں ان کا استعمال کیا
J-1 (Jurasic 1)(@lieberjurassic) LLM۔

## مزید

MRKL سسٹم کی [یہ مثال](https://python.langchain.com/docs/modules/agents/how_to/mrkl) دیکھیں
LangChain کے ساتھ بنایا گیا ہے۔
