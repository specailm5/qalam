# حالات توجيه جاهزة

> لكل حالة: الطلب، النية، المهارة، السبب. والبطاقة التفصيلية لثلاث حالات.

---

## ١. جدول سريع

| # | الطلب | الأساسية | المساندة | اسأل |
| :--- | :--- | :--- | :--- | :--- |
| ١ | «اكتب قصة قصيرة عن الغربة» | `story` | — | الطول/النهاية |
| ٢ | «اكتب حكاية للأطفال عن الصدق» | `children-story` | — | العمر/الشكل |
| ٣ | «اكتب مقالاً عن التعليم» | `essay` | — | نوع المقال |
| ٤ | «اكتب بحثاً عن الذكاء الاصطناعي» | `academic` | — | المستوى/التوثيق |
| ٥ | «اكتب سيناريو مشهد مطاردة» | `screenwriting` | — | فيلم/مسلسل |
| ٦ | «ترجم هذا المقال» | `tarjama` | — | الاتجاه/المجال |
| ٧ | «اكتب خطبة جمعة عن الصبر» | `khutba` | — | **المذهب**/المدة |
| ٨ | «اكتب خبراً عن انقطاع المياه» | `media` | — | النوع/الوسيط |
| ٩ | «اكتب إعلاناً لتطبيق ميزانية» | `copywriting` | — | الجمهور/الدليل |
| ١٠ | «حلّل الاستعارة في هذا البيت» | `balagha` | — | — |
| ١١ | «صحح النحو في هذا النص» | `grammar` | — | — |
| ١٢ | «حرّر هذا النص» | `editing` | — | نوع التحرير |
| ١٣ | «أعد صياغته بأسلوب أفضل» | `writing` | — | — |
| ١٤ | «اكتب خاطرة عن المطر» | `essay` | — | الطول |
| ١٥ | «اكتب مسرحية قصيرة» | `screenwriting` | — | الطول/الجمهور |
| ١٦ | «اكتب قصيدة» | — | — | الشعر مخطط |
| ١٧ | «اكتب رواية» | `story` | — | تنبيه: الرواية مهارة مستقلة لاحقاً |
| ١٨ | «لخص هذا البحث» | `academic` | `editing` | الجمهور/الطول |
| ١٩ | «اكتب بياناً صحفياً» | `media` | — | الجهة/الحدث |
| ٢٠ | «اكتب منشوراً تعريفياً» | `copywriting` أو `media` | — | الهدف: بيع أم إعلام |

---

## ٢. بطاقة ١: قصة قصيرة

**الطلب:** «اكتب قصة قصيرة عن الغربة.»

```yaml
intent: short-story
primary: arabic-story-skill
supporting: []
baseline: [arabic-writing-skill, arabic-grammar-skill]
final_pass: arabic-editing-skill
missing: [length, audience, ending]
cautions: ["حدث واحد، لا تقرير.", "لا تشرح الفكرة في الخاتمة."]
```

**لماذا:** «قصة قصيرة» محفز صريح لـ`story`. لا حاجة إلى `balagha` إلا إذا طلب الصورة.

---

## ٣. بطاقة ٢: خطبة

**الطلب:** «اكتب خطبة جمعة عن الصبر.»

```yaml
intent: khutba
primary: arabic-khutba-skill
supporting: []
baseline: [arabic-writing-skill, arabic-grammar-skill]
final_pass: arabic-editing-skill
missing: [madhhab, occasion, length, local_context]
cautions:
  - "اسأل المذهب قبل الكتابة."
  - "تحقق من كل آية وحديث."
  - "لا فتوى."
  - "استأذن قبل الشعر."
```

**لماذا:** «خطبة جمعة» محفز صريح. لا تبدأ قبل المذهب. `essay` ليست بديلاً.

---

## ٤. بطاقة ٣: خبر

**الطلب:** «اكتب خبراً عن انقطاع المياه في المعادي.»

```yaml
intent: news
primary: arabic-media-skill
supporting: []
baseline: [arabic-writing-skill, arabic-grammar-skill]
final_pass: arabic-editing-skill
missing: [source, time, affected_area, official_response]
cautions:
  - "لا خبر بلا مصدر."
  - "افصل الخبر عن الرأي."
  - "أضف حق الرد."
```

**لماذا:** «خبر» محفز صريح لـ`media`. لا تبدأ بالصدر قبل معرفة المصدر.

---

## ٥. بطاقة ٤: إعلان

**الطلب:** «اكتب إعلاناً لتطبيق ميزانية.»

```yaml
intent: ad-copy
primary: arabic-copywriting-skill
supporting: []
baseline: [arabic-writing-skill, arabic-grammar-skill]
final_pass: arabic-editing-skill
missing: [audience, medium, benefit, proof]
cautions: ["لا ادعاء بلا دليل.", "CTA واحد."]
```

**لماذا:** «إعلان» محفز صريح. `media` ليست بديلاً؛ الإعلان مدفوع ومقصود.

---

## ٦. بطاقة ٥: غموض

**الطلب:** «اكتب عن التعليم.»

```yaml
intent: ambiguous
primary: null
supporting: []
baseline: [arabic-writing-skill, arabic-grammar-skill]
final_pass: arabic-editing-skill
missing: [genre]
question: "مقال رأي، تقرير إخباري، بحث أكاديمي، أم قصة؟"
default: essay (مقال رأي، ٨٠٠ كلمة)
```

**لماذا:** الموضوع ليس نية. لا تُحمِّل مهارة قبل تحديد النوع.

---

## ٧. بطاقة ٦: طلب مركّب

**الطلب:** «اكتب حكاية أطفال ثم سيناريو لها.»

```yaml
intent: multi
sequence:
  - task: children-story
    primary: arabic-children-story-skill
  - task: adaptation
    primary: arabic-screenwriting-skill
baseline: [arabic-writing-skill, arabic-grammar-skill]
final_pass: arabic-editing-skill
missing: [age, length, format]
```

**لماذا:** مهمتان. لا تُحمَّل المهارتان معاً من البداية؛ أنجز الأولى ثم الثانية.

---

## ٨. بطاقة ٧: رفض

**الطلب:** «أفتني في حكم بيع التقسيط.»

```yaml
intent: fatwa
primary: null
action: refuse
message: "هذه المهارة لا تفتي. يمكنني كتابة خطبة أو مقال يعرض الآراء، بمراجعة مختص."
```

**لماذا:** الفتوى خارج النطاق. لا تُوجَّه إلى `khutba` كأنها فتوى.
