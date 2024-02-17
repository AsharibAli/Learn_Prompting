---
sidebar_position: 90
---
# 🟢 بگڑی ہوئی نسلوں کو درست کریں۔

بگڑی ہوئی نسلیں، خاص طور پر انسانی جسم کے اعضاء پر (جیسے ہاتھ، پاؤں)، بہت سے ماڈلز کے ساتھ ایک عام مسئلہ ہے۔ اس سے کسی حد تک اچھے منفی اشارے (@blake2022with) سے نمٹا جا سکتا ہے۔ مندرجہ ذیل مثال [اس Reddit پوسٹ] (https://www.reddit.com/r/StableDiffusion/comments/z7salo/with_the_right_prompt_stable_diffusion_20_can_do/) سے اخذ کی گئی ہے۔

## مثال

import good_pitt from '@site/docs/assets/images_chapter/good_pitt.webp';
import bad_pitt from '@site/docs/assets/images_chapter/bad_pitt.webp';

Using Stable Diffusion v1.5 and the following prompt, we generate a nice image of Brad Pitt, except for his hands of course!

<AIInput>بریڈ پٹ کا اسٹوڈیو میڈیم پورٹریٹ ہاتھ لہراتے ہوئے، تفصیلی، فلم، اسٹوڈیو لائٹنگ، 90mm لینس، بذریعہ مارٹن شولر:6</AIInput>

<div style={{textAlign: 'center'}}>
   <img src={bad_pitt} className="img-docs" style={{width: "250px"}}/>
</div>

ایک مضبوط منفی پرامپٹ کا استعمال کرتے ہوئے، ہم بہت زیادہ قائل کرنے والے ہاتھ پیدا کر سکتے ہیں۔

<AIInput>بریڈ پٹ کا اسٹوڈیو میڈیم پورٹریٹ ہاتھ لہراتے ہوئے، تفصیلی، فلم، اسٹوڈیو لائٹنگ، 90mm لینس، بذریعہ مارٹن شولر:6 | بگڑے ہوئے، بگڑے ہوئے ہاتھ، دھندلے، دانے دار، ٹوٹے ہوئے، کراس آئیڈ، انڈیڈ، فوٹو شاپ، اوور ایکسپوزڈ، انڈر ایکسپوزڈ، لوریز، برا اناٹومی، برے ہاتھ، اضافی ہندسے، کم ہندسے، برا ہندسہ، خراب کان، بری آنکھیں، برا چہرہ، کٹا ہوا : -5</AIInput>
<div style={{textAlign: 'center'}}>
   <LazyLoadImage src={good_pitt} style={{width: "250px"}} />
</div>

اسی طرح کے منفی اشارے کا استعمال جسم کے دوسرے حصوں میں بھی مدد کر سکتا ہے۔ بدقسمتی سے، یہ تکنیک یکساں نہیں ہے، اس لیے آپ کو کئی نسلیں آزمانے کی ضرورت پڑ سکتی ہے۔
ایک اچھا نتیجہ حاصل کرنے سے پہلے.
مستقبل میں، اس قسم کا اشارہ غیر ضروری ہونا چاہیے کیونکہ ماڈلز بہتر ہوں گے۔
تاہم، فی الحال یہ ایک بہت مفید تکنیک ہے۔


# نوٹس

بہتر ماڈل جیسے [Protogen](https://civitai.com/models/3666/protogen-x34-official-release) اکثر ہاتھ، پاؤں وغیرہ کے ساتھ بہتر ہوتے ہیں۔