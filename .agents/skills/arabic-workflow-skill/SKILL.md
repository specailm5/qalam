---
name: arabic-workflow-skill
description: "Intent router and workflow skill for the Arabic skill suite. Loads first, identifies what the user actually wants (genre, deliverable, audience, medium, risk), then selects the smallest correct set of Arabic skills and their load order. Keeps arabic-writing-skill (anti-العرنجية) and arabic-grammar-skill as the always-on baseline, adds arabic-editing-skill as the final pass, and routes to story, screenwriting, children's tales, essay, academic, translation, khutba, media, copywriting or balagha only when the request requires them. Contains the registry of all skill repository URLs and install commands. Does not write the content itself. Use when the user asks for any Arabic writing, editing, translation, analysis or religious/media/academic text and you must decide which skill(s) to load. Triggers: «أي مهارة»، «وجّه الطلب»، «اختر المهارة»، «workflow»، «router»، «which skill»، or any open-ended Arabic writing request."
license: MIT
metadata:
    type: meta-skill
    role: intent-router
    version: 1.0.0
    registry-schema: 1
    always-load: arabic-writing-skill, arabic-grammar-skill
    final-pass: arabic-editing-skill
    github-path: .agents/skills/arabic-workflow-skill
    github-ref: refs/heads/master
    github-repo: https://github.com/specailm5/arabic-workflow-skill
---

# مهارة توجيه المهارات العربية

> **دورها:** تُحمَّل أولاً، تفهم الطلب، تختار المهارات، ثم تسلّم.
> **لا تكتب المحتوى بنفسها.** ولا تُحمِّل كل المهارات. ولا تُخمِّن النية بلا دليل.

> **قاعدة التحميل:** `arabic-writing-skill` + `arabic-grammar-skill` دائماً. ثم مهارة واحدة أساسية. ثم `arabic-editing-skill` قبل التسليم. وأي مهارة أخرى بالحاجة فقط.

---

## ٠. لماذا هذه المهارة قصيرة؟

مهارة التوجيه تُحمَّل قبل كل شيء، فلو كانت ٣٠ ألف حرف لأكلت سياق النموذج قبل أن يبدأ. لذلك:

- **`SKILL.md`:** قواعد التوجيه فقط.
- **`references/registry.json`:** بيانات كل مهارة (الروابط، التثبيت، المحفزات، الأسئلة، التحذيرات).
- **`references/routing_rules.md`:** قواعد الاختيار والتعارض.
- **`references/ambiguity.md`:** أسئلة فك الالتباس.
- **`examples/`:** حالات جاهزة.

**هذه مهارة ميتا (meta-skill)، وليست مهارة كتابة.** لا تنطبق عليها قاعدة «٢–٤ كتب»؛ لأنها لا تُعلِّم بلاغة ولا نحواً، بل تُوجِّه إلى من يُعلِّم.

---

## ١. أول ٣٠ ثانية: استخراج النية

لا تبدأ بالكتابة. استخرج six إشارات:

| الإشارة | السؤال | مثال |
| :--- | :--- | :--- |
| **النوع** | ما جنس النص؟ | قصة، مقال، خبر، خطبة، ترجمة |
| **المخرج** | ماذا يريد؟ | مسودة، مخطط، نقد، تحرير، ترجمة |
| **الجمهور** | لمن؟ | حكايات أطفال، أكاديميون، جمهور عام |
| **الوسيط** | أين؟ | مطبوع، موقع، فيلم، مسرح، سوشيال |
| **اللغة** | بأي لغة؟ | عربية، إنجليزية، ثنائية |
| **الخطر** | ما المحظور؟ | دين، طب، قانون، وقائع، حكايات أطفال |

### ١.١ بطاقة النية

```yaml
intent: ...
deliverable: draft | outline | critique | edit | translate | analyze
genre: ...
audience: ...
medium: ...
language: ar | en | both
risk: none | religious | medical | legal | factual | minors
```

**قاعدة:** إن غابت إشارة، لا تسأل عنها كلها. اسأل عن **الإشارة التي تغيّر المهارة** فقط.

- الجمهور يغيّر المهارة: «قصة» لطفل ≠ «قصة» لبالغ.
- الوسيط يغيّر المهارة: «مشهد» لفيلم ≠ «مشهد» في رواية.
- المخرج يغيّر المهارة: «راجع» قد تعني تحريراً أو نقداً أو مراجعة أكاديمية.

---

## ٢. خريطة النوايا

| النية | المهارة الأساسية | مساندة عند الحاجة | اسأل أولاً |
| :--- | :--- | :--- | :--- |
| تحسين لغة/أسلوب | `arabic-writing-skill` | `arabic-balagha-skill` | — |
| نحو/إعراب | `arabic-grammar-skill` | `arabic-writing-skill` | — |
| تحرير/تدقيق | `arabic-editing-skill` | `arabic-writing-skill` | نوع التحرير |
| صورة/بلاغة | `arabic-balagha-skill` | `arabic-writing-skill` | تحليل أم إنتاج |
| قصة/رواية | `arabic-story-skill` | `arabic-balagha-skill` | الطول/الجمهور |
| سيناريو/مسرح | `arabic-screenwriting-skill` | `arabic-story-skill` | الصيغة/الطول |
| حكايات الأطفال واليافعين | `arabic-children-story-skill` | `arabic-story-skill` | العمر/الشكل |
| مقال/عمود/خاطرة | `arabic-essay-skill` | `arabic-balagha-skill` | النوع/الطول |
| بحث/رسالة | `arabic-academic-skill` | `arabic-editing-skill` | المستوى/التوثيق |
| ترجمة | `arabic-tarjama-skill` | `arabic-writing-skill` | الاتجاه/المجال |
| خطبة | `arabic-khutba-skill` | `arabic-essay-skill` | المذهب/المناسبة |
| خبر/تقرير/تحقيق | `arabic-media-skill` | `arabic-editing-skill` | النوع/الوسيط |
| إعلان/تسويق | `arabic-copywriting-skill` | `arabic-media-skill` | المنتج/الوسيط |

**قاعدة:** النية تحدد المهارة، لا الموضوع. «اكتب عن التعليم» ليست نية؛ «اكتب مقال رأي عن التعليم» نية.

---

## ٣. قواعد الاختيار الخمس

### ٣.١ مهارة أساسية واحدة

اختر **مهارة أساسية واحدة** لكل مهمة. لا تخلط قصيدة مع سيناريو، ولا مقالاً مع بحث.

### ٣.٢ خط الأساس دائماً

- `arabic-writing-skill`: يضبط اللغة ونبذ العَرَنْجِيَّة.
- `arabic-grammar-skill`: يضبط النحو والإعراب.
- `arabic-editing-skill`: يمرّ قبل التسليم.

**لا تطلب من المستخدم تثبيتها كل مرة.** إن كانت مثبتة، استخدمها. وإن لم تكن، ثبّتها أو اطلب الإذن.

### ٣.٣ المساندة بالحاجة

لا تضف مهارة مساندة إلا إذا طلبها الطلب صراحةً أو احتاجها النص:

- «حسّن الصورة» → `balagha`.
- «دقّق المصادر» → `editing`.
- «حوّلها إلى مشهد» → `screenwriting`.
- «اكتبها حكاية للأطفال» → `children-story`.

### ٣.٤ الطلب المركّب يُقسَّم

«اكتب حكاية أطفال ثم سيناريو لها» = مهمتان:

```text
① children-story → ② screenwriting
```

لا تُحمِّل المهارتين معاً من البداية. أنجز الأولى، ثم انتقل.

### ٣.٥ الغموض يُحل بسؤال واحد

إن كان الطلب يحتمل مهارتين، اسأل سؤالاً واحداً بخيارين أو ثلاثة. لا تستجوب المستخدم.

---

## ٤. ترتيب التحميل

### ٤.١ عند الإنشاء

```text
① arabic-writing-skill      (خط الأساس اللغوي)
② arabic-grammar-skill      (ضبط الجملة)
③ المهارة الأساسية          (النوع)
④ المساندة                  (عند الحاجة)
⑤ arabic-editing-skill      (قبل التسليم)
```

### ٤.٢ عند المراجعة

```text
① arabic-editing-skill      (تشخيص)
② المهارة الأساسية          (إن كان الخلل بنيوياً)
③ arabic-writing-skill      (الأسلوب)
④ arabic-grammar-skill      (النحو)
```

### ٤.٣ عند الترجمة

```text
① arabic-tarjama-skill
② arabic-writing-skill
③ arabic-grammar-skill
④ arabic-editing-skill
```

### ٤.٤ عند الخطبة

```text
① اسأل عن المذهب والمناسبة.
② arabic-khutba-skill
③ arabic-writing-skill
④ arabic-grammar-skill
⑤ arabic-editing-skill
```

**قاعدة:** لا تُحمِّل `editing` قبل وجود نص. ولا تُحمِّل `balagha` قبل معرفة النوع.

---

## ٥. بطاقة التوجيه (المخرج الإلزامي)

قبل أي تحميل أو كتابة، أخرج بطاقة قصيرة:

```yaml
intent: short-story
primary: arabic-story-skill
supporting: []
baseline:
  - arabic-writing-skill
  - arabic-grammar-skill
final_pass: arabic-editing-skill
order:
  - arabic-writing-skill
  - arabic-grammar-skill
  - arabic-story-skill
  - arabic-editing-skill
missing:
  - length
  - audience
cautions:
  - "لا تحوّل القصة إلى تقرير."
```

**قاعدة:** البطاقة للمستخدم/الوكيل، لا للنشر. اجعلها قصيرة.

---

## ٦. أمثلة سريعة

| الطلب | الأساسية | المساندة | ملاحظة |
| :--- | :--- | :--- | :--- |
| «اكتب قصة قصيرة عن الغربة» | `story` | — | اسأل الطول إن لزم |
| «اكتب حكاية للأطفال عن النظافة» | `children-story` | — | اسأل العمر |
| «اكتب مقالاً عن التعليم» | `essay` | — | اسأل نوع المقال |
| «اكتب بحثاً عن الذكاء الاصطناعي» | `academic` | — | اسأل المستوى والتوثيق |
| «اكتب سيناريو مشهد» | `screenwriting` | — | اسأل الفيلم/المسلسل |
| «ترجم هذا النص» | `tarjama` | — | اسأل الاتجاه |
| «اكتب خطبة جمعة» | `khutba` | — | اسأل المذهب أولاً |
| «اكتب خبراً عن حادث» | `media` | — | تحقق من المصادر |
| «اكتب إعلاناً لتطبيق» | `copywriting` | — | اسأل الجمهور والدليل |
| «حلّل هذه الاستعارة» | `balagha` | — | — |
| «صحح النحو» | `grammar` | — | — |
| «حرّر هذا النص» | `editing` | — | — |
| «أعد صياغته بأسلوب أفضل» | `writing` | — | — |
| «اكتب قصيدة» | — | — | الشعر مخطط، غير منشور بعد |

**قاعدة:** إن كان الطلب «اكتب نصاً» بلا نوع، اسأل: «قصة، مقال، خبر، أم نص آخر؟» ولا تفترض.

---

## ٧. الأسئلة الحاسمة

| المهارة | السؤال | لماذا؟ |
| :--- | :--- | :--- |
| `story` | الطول؟ الجمهور؟ النهاية؟ | يحدد البنية |
| `screenwriting` | فيلم/مسلسل/مسرح؟ الطول؟ | يحدد الصيغة |
| `children-tales` | العمر؟ كتاب مصور/حكاية؟ | يحدد المفردات |
| `essay` | مقال أدبي/رأي/عمود/خاطرة؟ | يحدد الصوت |
| `academic` | المستوى؟ التوثيق؟ | يحدد البنية |
| `tarjama` | الاتجاه؟ المجال؟ | يحدد المصطلح |
| `khutba` | المذهب؟ المناسبة؟ | يحدد الفقه |
| `media` | خبر/تقرير/تحقيق/حوار؟ | يحدد الأسلوب |
| `copywriting` | المنتج؟ الجمهور؟ الوسيط؟ الدليل؟ | يحدد الفكرة |
| `balagha` | تحليل أم إنتاج؟ | يحدد المخرج |

**قاعدة:** سؤال واحد لكل غموض. ولا تسأل عن معلومة موجودة في الطلب.

---

## ٨. الأخطاء الشائعة

| # | الخطأ | العلاج |
| :--- | :--- | :--- |
| ١ | تحميل كل المهارات | مهارة أساسية + خط الأساس |
| ٢ | اختيار الموضوع بدل النية | «عن التعليم» ليست نوعاً |
| ٣ | تخطي خط الأساس | writing + grammar دائماً |
| ٤ | تخطي التحرير | editing قبل التسليم |
| ٥ | خلط جنسين | قسّم المهمة |
| ٦ | افتراض الجمهور | اسأل إن غاب |
| ٧ | خطبة بلا مذهب | اسأل أولاً |
| ٨ | ترجمة بلا اتجاه | اسأل أولاً |
| ٩ | كتابة المحتوى بدل التوجيه | سلّم للمهارة |
| ١٠ | استجواب المستخدم | سؤال واحد |
| ١١ | تحميل `balagha` لكل نص | عند طلب الصورة فقط |
| ١٢ | تحميل `editing` قبل النص | بعد المسودة |
| ١٣ | استخدام `media` للمقال | المقال عند `essay` |
| ١٤ | استخدام `essay` للخبر | الخبر عند `media` |
| ١٥ | نسيان التحذيرات | دين/طب/قانون/وقائع |

---

## ٩. الحدود

1. **لا تكتب المحتوى.** التوجيه ليس إنشاءً.
2. **لا تُفتِ.** الخطبة تُعرض ولا تُفتي.
3. **لا تختلق مصادر** أو وقائع.
4. **لا تُقدّم استشارة طبية/قانونية.**
5. **لا تُحمِّل مهارة غير مسجّلة** في `registry.json`.
6. **لا تَعِد بمهارة مخطط لها** كأنها منشورة.
7. **لا تتجاوز سؤال المذهب** في الخطبة.
8. **لا تتجاهل الخطر** في حكايات الأطفال أو الوقائع.

---

## ١٠. سجل المهارات

الجدول الكامل بالروابط وأوامر التثبيت في `references/skill_registry.md` و`references/registry.json`. المهارات النشطة:

| المهارة | الدور | المستودع |
| :--- | :--- | :--- |
| `arabic-writing-skill` | خط أساس | <https://github.com/specailm5/arabic-writing-skill> |
| `arabic-grammar-skill` | خط أساس | <https://github.com/specailm5/arabic-grammar-skill> |
| `arabic-editing-skill` | تمرير نهائي | <https://github.com/specailm5/arabic-editing-skill> |
| `arabic-balagha-skill` | بلاغة | <https://github.com/specailm5/arabic-balagha-skill> |
| `arabic-story-skill` | قصة | <https://github.com/specailm5/arabic-story-skill> |
| `arabic-screenwriting-skill` | سيناريو | <https://github.com/specailm5/arabic-screenwriting-skill> |
| `arabic-children-story-skill` | حكايات أطفال | <https://github.com/specailm5/arabic-children-story-skill> |
| `arabic-essay-skill` | مقال | <https://github.com/specailm5/arabic-essay-skill> |
| `arabic-academic-skill` | أكاديمي | <https://github.com/specailm5/arabic-academic-skill> |
| `arabic-tarjama-skill` | ترجمة | <https://github.com/specailm5/arabic-tarjama-skill> |
| `arabic-khutba-skill` | خطبة | <https://github.com/specailm5/arabic-khutba-skill> |
| `arabic-media-skill` | إعلام | <https://github.com/specailm5/arabic-media-skill> |
| `arabic-copywriting-skill` | إعلان | <https://github.com/specailm5/arabic-copywriting-skill> |

**المخطط لها (ليست منشورة):** الشعر، الرواية الطويلة، المسرح، الحكايات المصورة، الحكايات التفاعلية.

---

## ١١. التثبيت

```bash
# ١. مهارة التوجيه
npx skills add specailm5/arabic-workflow-skill -g -y

# ٢. خط الأساس (إلزامي)
npx skills add specailm5/arabic-writing-skill -g -y
npx skills add specailm5/arabic-grammar-skill -g -y

# ٣. التمرير النهائي
npx skills add specailm5/arabic-editing-skill -g -y

# ٤. المهارة النوعية عند الحاجة
npx skills add specailm5/arabic-story-skill -g -y
```

**قاعدة:** لا تثبّت الـ١٣ كلها. ثبّت خط الأساس + ما تستخدمه فعلاً.

---

## ١٢. إضافة مهارة جديدة

1. أضف سجلاً في `references/registry.json`:
   - `id`, `repo`, `title_ar`, `summary`
   - `triggers_ar`, `triggers_en`
   - `primary_for`, `always_load`, `final_pass`
   - `requires_questions`, `cautions`
   - `install`, `docs`, `repo_url`, `raw`, `status`
2. أضف صفاً في `references/skill_registry.md`.
3. أضف صفاً في جدول الباب ١٠.
4. اختبر خمس حالات توجيه.
5. ارفع `version` في frontmatter.

**قاعدة:** لا تُضف مهارة بلا رابط مستودع و`raw` وتثبيت. المخطط لها تُسجَّل في `planned` بلا رابط.

---

## ١٣. المراجع

- `references/registry.json` — سجل الآلة.
- `references/skill_registry.md` — سجل بشري بالروابط.
- `references/routing_rules.md` — قواعد التعارض والترتيب.
- `references/ambiguity.md` — أسئلة فك الالتباس.
- `examples/routing_cases.md` — حالات جاهزة.
- `examples/multi_skill_requests.md` — الطلبات المركّبة.

> **إقرار:** هذه مهارة توجيه، لا تُعلِّم جنساً أدبياً. والفضل في كل جنس لمهارته ومصادره.
