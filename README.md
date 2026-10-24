# قلم (Qalam)

**قلم** يقرأ طلبك العربي، ويختار المهارات التي تكتبه ويرتّبها — فلا تحتاج إلى حفظ أسماء المهارات ولا ترتيبها.

<p align="center">
  <a href="https://github.com/specailm5/qalam/blob/master/LICENSE"><img alt="License" src="https://img.shields.io/github/license/specailm5/qalam?style=flat-square"></a>
  <a href="https://github.com/specailm5/qalam/commits/master"><img alt="Last commit" src="https://img.shields.io/github/last-commit/specailm5/qalam?style=flat-square"></a>
  <a href="https://specailm5.github.io/qalam/"><img alt="Docs" src="https://img.shields.io/badge/docs-live-brightgreen?style=flat-square"></a>
  <img alt="Agent Skills" src="https://img.shields.io/badge/Agent%20Skills-compatible-5B21B6?style=flat-square">
  <img alt="Meta skill" src="https://img.shields.io/badge/type-meta--skill-0F766E?style=flat-square">
</p>

🔗 **الموقع المرجعي (السجل والتوجيه والأمثلة): [specailm5.github.io/qalam](https://specailm5.github.io/qalam/)**

> **English:** an intent router for the Arabic skill suite. It reads the request, picks the right skills, and loads them in order. Works with Claude Code, Codex, Antigravity and VS Code agent harnesses.

---

## 📖 ماذا يفعل قلم؟

تكتب طلبك كما تتكلم:

> «اكتب حكاية للأطفال عن الصدق»

فيقرأ قلم الطلب، ويحدد: النوع (حكاية أطفال)، وما يلزمه من لغة ونحو، والتحرير قبل التسليم. ثم يعرض بطاقة التوجيه، ويسأل عن العمر — لأنه يغيّر النتيجة — ويبدأ العمل بالمهارة الصحيحة.

**ما تحصل عليه:**

- اختيار صحيح من أول مرة، بدل تجربة مهارة بعد أخرى.
- أسئلة قليلة، لا تُسأل إلا عمّا يغيّر النتيجة.
- ترتيب ثابت: لغة، ثم نحو، ثم المهارة، ثم تحرير.

---

## ⚡ ابدأ في دقيقة

### المتطلبات

- **وكيل يدعم Agent Skills** — Claude Code، Codex، Antigravity، أو VS Code agent harness.
- **Node.js 22.20 أو أحدث مع `npx`** — لتشغيل مثبّت `skills`.
- **مهارتا خط الأساس** — `arabic-writing-skill` و`arabic-grammar-skill`، ويُضاف إليهما `arabic-editing-skill` للتمرير النهائي.

### ١. ثبّت قلم وخط الأساس

```bash
npx skills add specailm5/qalam -g -y
npx skills add specailm5/arabic-writing-skill -g -y
npx skills add specailm5/arabic-grammar-skill -g -y
npx skills add specailm5/arabic-editing-skill -g -y
```

### ٢. تحقق من التثبيت

```bash
npx skills list
```

### ٣. أول نتيجة

اكتب في وكيلك:

> «اكتب قصة قصيرة عن الغربة»

فيعرض قلم بطاقة التوجيه قبل أن يبدأ:

```yaml
intent: short-story
primary: arabic-story-skill
supporting: []
baseline: [arabic-writing-skill, arabic-grammar-skill]
final_pass: arabic-editing-skill
missing: [length, audience, ending]
cautions: ["حدث واحد، لا تقرير.", "لا تشرح الفكرة في الخاتمة."]
```

ثم يسأل عمّا ينقص (`missing`)، ويحمّل `arabic-story-skill` بعد خط الأساس، ويمرّر `arabic-editing-skill` قبل التسليم.

### ثبّت المهارة النوعية التي تحتاجها فقط

```bash
npx skills add specailm5/arabic-story-skill -g -y
npx skills add specailm5/arabic-children-story-skill -g -y
npx skills add specailm5/arabic-essay-skill -g -y
```

<details>
<summary>التثبيت اليدوي (بدون <code>npx</code>)</summary>

**Windows**

```powershell
$src = "skills\qalam"

New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.claude\skills\qalam"
Copy-Item -Recurse -Force "$src\*" "$env:USERPROFILE\.claude\skills\qalam\"

New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.agents\skills\qalam"
Copy-Item -Recurse -Force "$src\*" "$env:USERPROFILE\.agents\skills\qalam\"
```

**macOS / Linux**

```bash
src=skills/qalam

mkdir -p ~/.claude/skills/qalam
cp -r "$src/." ~/.claude/skills/qalam/

mkdir -p ~/.agents/skills/qalam
cp -r "$src/." ~/.agents/skills/qalam/
```

**بدون بيئة برمجية:** انسخ محتوى [`skills/qalam/SKILL.md`](skills/qalam/SKILL.md) إلى التعليمات المخصصة أو System Prompt، وثبّت خط الأساس.

</details>

---

## 🧱 ما يُحمَّل مع كل طلب

<table dir="rtl" align="right">
<thead>
<tr>
<th align="right">المهارة</th>
<th align="right">الدور</th>
<th align="right">متى</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>arabic-writing-skill</code></td>
<td><strong>دائماً</strong></td>
<td>كل نص عربي — الأسلوب ونبذ العَرَنْجِيَّة</td>
</tr>
<tr>
<td><code>arabic-grammar-skill</code></td>
<td><strong>دائماً</strong></td>
<td>كل نص عربي — النحو والإعراب</td>
</tr>
<tr>
<td><code>arabic-editing-skill</code></td>
<td><strong>قبل التسليم</strong></td>
<td>إلا إذا طُلبت مسودة سريعة</td>
</tr>
</tbody>
</table>
<br clear="all">

---

## 🗂️ المهارات المتاحة

<table dir="rtl" align="right">
<thead>
<tr>
<th align="right">المهارة</th>
<th align="right">النية</th>
<th align="right">المستودع</th>
<th align="right">الموقع</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>arabic-writing-skill</code></td>
<td>لغة/أسلوب</td>
<td><a href="https://github.com/specailm5/arabic-writing-skill">GitHub</a></td>
<td><a href="https://specailm5.github.io/arabic-writing-skill/">docs</a></td>
</tr>
<tr>
<td><code>arabic-grammar-skill</code></td>
<td>نحو/إعراب</td>
<td><a href="https://github.com/specailm5/arabic-grammar-skill">GitHub</a></td>
<td><a href="https://specailm5.github.io/arabic-grammar-skill/">docs</a></td>
</tr>
<tr>
<td><code>arabic-editing-skill</code></td>
<td>تحرير/تدقيق</td>
<td><a href="https://github.com/specailm5/arabic-editing-skill">GitHub</a></td>
<td><a href="https://specailm5.github.io/arabic-editing-skill/">docs</a></td>
</tr>
<tr>
<td><code>arabic-balagha-skill</code></td>
<td>بلاغة/صورة</td>
<td><a href="https://github.com/specailm5/arabic-balagha-skill">GitHub</a></td>
<td><a href="https://specailm5.github.io/arabic-balagha-skill/">docs</a></td>
</tr>
<tr>
<td><code>arabic-story-skill</code></td>
<td>قصة/رواية</td>
<td><a href="https://github.com/specailm5/arabic-story-skill">GitHub</a></td>
<td><a href="https://specailm5.github.io/arabic-story-skill/">docs</a></td>
</tr>
<tr>
<td><code>arabic-screenwriting-skill</code></td>
<td>سيناريو/مسرح</td>
<td><a href="https://github.com/specailm5/arabic-screenwriting-skill">GitHub</a></td>
<td><a href="https://specailm5.github.io/arabic-screenwriting-skill/">docs</a></td>
</tr>
<tr>
<td><code>arabic-children-story-skill</code></td>
<td>حكايات الأطفال واليافعين</td>
<td><a href="https://github.com/specailm5/arabic-children-story-skill">GitHub</a></td>
<td><a href="https://specailm5.github.io/arabic-children-story-skill/">docs</a></td>
</tr>
<tr>
<td><code>arabic-essay-skill</code></td>
<td>مقال/خاطرة</td>
<td><a href="https://github.com/specailm5/arabic-essay-skill">GitHub</a></td>
<td><a href="https://specailm5.github.io/arabic-essay-skill/">docs</a></td>
</tr>
<tr>
<td><code>arabic-academic-skill</code></td>
<td>بحث/توثيق</td>
<td><a href="https://github.com/specailm5/arabic-academic-skill">GitHub</a></td>
<td><a href="https://specailm5.github.io/arabic-academic-skill/">docs</a></td>
</tr>
<tr>
<td><code>arabic-tarjama-skill</code></td>
<td>ترجمة</td>
<td><a href="https://github.com/specailm5/arabic-tarjama-skill">GitHub</a></td>
<td><a href="https://specailm5.github.io/arabic-tarjama-skill/">docs</a></td>
</tr>
<tr>
<td><code>arabic-khutba-skill</code></td>
<td>خطبة</td>
<td><a href="https://github.com/specailm5/arabic-khutba-skill">GitHub</a></td>
<td><a href="https://specailm5.github.io/arabic-khutba-skill/">docs</a></td>
</tr>
<tr>
<td><code>arabic-media-skill</code></td>
<td>إعلام</td>
<td><a href="https://github.com/specailm5/arabic-media-skill">GitHub</a></td>
<td><a href="https://specailm5.github.io/arabic-media-skill/">docs</a></td>
</tr>
<tr>
<td><code>arabic-copywriting-skill</code></td>
<td>إعلان</td>
<td><a href="https://github.com/specailm5/arabic-copywriting-skill">GitHub</a></td>
<td><a href="https://specailm5.github.io/arabic-copywriting-skill/">docs</a></td>
</tr>
</tbody>
</table>
<br clear="all">

أمر التثبيت لكل مهارة: `npx skills add specailm5/<اسم-المهارة> -g -y`

**قادم:** الشعر، الرواية الطويلة، المسرح، الحكايات المصورة، الحكايات التفاعلية.

---

## 🧭 ما الذي يحدد الاختيار؟

<table dir="rtl" align="right">
<thead>
<tr>
<th align="right">ما تذكره</th>
<th align="right">مثال</th>
<th align="right">أثره</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>النوع</strong></td>
<td>قصة، مقال، خبر، خطبة</td>
<td>المهارة الأساسية</td>
</tr>
<tr>
<td><strong>المخرج</strong></td>
<td>مسودة، نقد، تحرير، ترجمة</td>
<td>هل الأساسية نوع أم تحرير</td>
</tr>
<tr>
<td><strong>الجمهور</strong></td>
<td>أطفال، أكاديميون، عام</td>
<td>يغيّر المهارة</td>
</tr>
<tr>
<td><strong>الوسيط</strong></td>
<td>مطبوع، فيلم، مسرح، سوشيال</td>
<td>يغيّر الصيغة</td>
</tr>
<tr>
<td><strong>اللغة</strong></td>
<td>عربية، إنجليزية، ثنائية</td>
<td>يحدد الترجمة</td>
</tr>
<tr>
<td><strong>المحظور</strong></td>
<td>دين، طب، قانون، أطفال</td>
<td>أسئلة وتحذيرات</td>
</tr>
</tbody>
</table>
<br clear="all">

كلما ذكرت النوع والجمهور والطول، قلّت الأسئلة.

### ترتيب التحميل

<pre dir="rtl"><code>
① arabic-writing-skill      (اللغة والأسلوب)
② arabic-grammar-skill      (ضبط الجملة)
③ المهارة الأساسية          (النوع)
④ المساندة                  (عند الحاجة)
⑤ arabic-editing-skill      (قبل التسليم)
</code></pre>

---

## 🧩 أمثلة

<table dir="rtl" align="right">
<thead>
<tr>
<th align="right">الطلب</th>
<th align="right">الأساسية</th>
<th align="right">ملاحظة</th>
</tr>
</thead>
<tbody>
<tr>
<td>«اكتب قصة قصيرة عن الغربة»</td>
<td><code>arabic-story-skill</code></td>
<td>اسأل الطول والنهاية</td>
</tr>
<tr>
<td>«اكتب حكاية للأطفال عن الصدق»</td>
<td><code>arabic-children-story-skill</code></td>
<td>اسأل العمر</td>
</tr>
<tr>
<td>«اكتب مقالاً عن التعليم»</td>
<td><code>arabic-essay-skill</code></td>
<td>اسأل نوع المقال</td>
</tr>
<tr>
<td>«اكتب بحثاً عن الذكاء الاصطناعي»</td>
<td><code>arabic-academic-skill</code></td>
<td>اسأل المستوى والتوثيق</td>
</tr>
<tr>
<td>«اكتب سيناريو مشهد مطاردة»</td>
<td><code>arabic-screenwriting-skill</code></td>
<td>اسأل فيلم/مسلسل</td>
</tr>
<tr>
<td>«ترجم هذا المقال»</td>
<td><code>arabic-tarjama-skill</code></td>
<td>اسأل الاتجاه</td>
</tr>
<tr>
<td>«اكتب خطبة جمعة عن الصبر»</td>
<td><code>arabic-khutba-skill</code></td>
<td><strong>اسأل المذهب أولاً</strong></td>
</tr>
<tr>
<td>«اكتب خبراً عن انقطاع المياه»</td>
<td><code>arabic-media-skill</code></td>
<td>تحقق من المصادر</td>
</tr>
<tr>
<td>«اكتب إعلاناً لتطبيق ميزانية»</td>
<td><code>arabic-copywriting-skill</code></td>
<td>اسأل الجمهور والدليل</td>
</tr>
<tr>
<td>«حلّل الاستعارة في هذا البيت»</td>
<td><code>arabic-balagha-skill</code></td>
<td>—</td>
</tr>
<tr>
<td>«صحح النحو في هذا النص»</td>
<td><code>arabic-grammar-skill</code></td>
<td>—</td>
</tr>
<tr>
<td>«حرّر هذا النص»</td>
<td><code>arabic-editing-skill</code></td>
<td>اسأل نوع التحرير</td>
</tr>
<tr>
<td>«أعد صياغته بأسلوب أفضل»</td>
<td><code>arabic-writing-skill</code></td>
<td>—</td>
</tr>
</tbody>
</table>
<br clear="all">

حالة «اكتب قصيدة» لا تُوجَّه إلى مهارة منشورة بعد. راجع [`examples/routing_cases.md`](skills/qalam/examples/routing_cases.md) لعشرين حالة كاملة.

---

## 📚 عن المشروع

قلم لا يكتب النص؛ يختار المهارة التي تكتبه. سجلّه الكامل — الروابط وأوامر التثبيت والمحفّزات — في [`references/registry.json`](skills/qalam/references/registry.json).

---

## 🤝 المساهمة

نرحب بالمساهمات التي تحسّن السجل أو قواعد التوجيه. اقرأ [CONTRIBUTING.md](CONTRIBUTING.md) قبل فتح طلب سحب، والتزم بـ[قواعد السلوك](CODE_OF_CONDUCT.md).

## 🛡️ الأمان

إن وجدت مشكلة أمنية، فلا تفتح قضية عامة؛ راجع [SECURITY.md](SECURITY.md).

## 📄 سجل التغييرات

راجع [CHANGELOG.md](CHANGELOG.md).

## 📬 الدعم

للأسئلة والاقتراحات: [افتح قضية](https://github.com/specailm5/qalam/issues).

---

## 📜 الترخيص

هذه المهارة مفتوحة المصدر تحت رخصة [MIT](LICENSE).
