# قلم (Qalam)

**مستودع مهارات للكتابة العربية** يضيفها إلى وكيلك الذكي، فتصحح أخطاءه في العربية، وتحسّن أسلوبه، وتكتب ما تطلبه: قصة، مقالاً، خبراً، خطبة، بحثاً، أو ترجمة.

<p align="center">
  <a href="https://github.com/specailm5/qalam/blob/master/LICENSE"><img alt="License" src="https://img.shields.io/github/license/specailm5/qalam?style=flat-square"></a>
  <a href="https://github.com/specailm5/qalam/commits/master"><img alt="Last commit" src="https://img.shields.io/github/last-commit/specailm5/qalam?style=flat-square"></a>
  <a href="https://specailm5.github.io/qalam/"><img alt="Docs" src="https://img.shields.io/badge/docs-live-brightgreen?style=flat-square"></a>
  <img alt="Agent Skills" src="https://img.shields.io/badge/Agent%20Skills-compatible-5B21B6?style=flat-square">
  <img alt="Arabic" src="https://img.shields.io/badge/language-Arabic-0F766E?style=flat-square">
</p>

🔗 **الموقع المرجعي (الأنواع والأمثلة والتفاصيل): [specailm5.github.io/qalam](https://specailm5.github.io/qalam/)**

> **English:** a repository of Arabic writing skills for AI agents. It fixes the model's Arabic errors, improves its style, and covers every kind of Arabic writing. Works with Claude Code, Codex, Antigravity and VS Code agent harnesses.

---

## 📖 ماذا يعطيك قلم؟

وكيلك يكتب بالعربية، لكنه يخطئ: يترجم حرفياً، ويستعمل لغة الإنشاءات، ويخلط بين أنواع الكتابة. بعد تثبيت قلم:

- **أسلوب عربي طبيعي** — بعيد عن الترجمة الحرفية والعَرَنْجِيَّة.
- **نحو وإعراب مضبوطان** — يصحح الجملة قبل أن يسلّمها.
- **لكل نوع أصوله** — القصة لها بناؤها، والخبر له بنيته، والخطبة لها فقهها، والبحث له توثيقه.
- **مراجعة قبل التسليم** — يصلك النص محرَّراً، لا مسودة تحتاج تصحيحاً منك.
- **أسئلة قليلة** — لا يسأل إلا عمّا يغيّر النتيجة: العمر في حكاية الأطفال، والمذهب في الخطبة، والجمهور في الإعلان.

---

## ⚡ ابدأ في دقيقة

### المتطلبات

- **وكيل يدعم Agent Skills** — Claude Code، Codex، Antigravity، أو VS Code agent harness.
- **Node.js 22.20 أو أحدث مع `npx`** — لتشغيل مثبّت `skills`.

### ١. ثبّت قلم مع أساس اللغة

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

> «اكتب حكاية للأطفال عن الصدق»

فيسألك عن العمر، ثم يكتب الحكاية بأسلوب عربي سليم، ويراجعها قبل أن يسلّمها.

### أضف الأنواع التي تحتاجها

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

**بدون بيئة برمجية:** انسخ محتوى [`skills/qalam/SKILL.md`](skills/qalam/SKILL.md) إلى التعليمات المخصصة أو System Prompt، ومعه مهارات الأساس.

</details>

---

## 🗂️ الأنواع

<table dir="rtl" align="right">
<thead>
<tr>
<th align="right">النوع</th>
<th align="right">ما تحصل عليه</th>
<th align="right">التفاصيل</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>لغة وأسلوب</strong></td>
<td>صياغة عربية سليمة، بلا ترجمة حرفية ولا عَرَنْجِيَّة</td>
<td><a href="https://specailm5.github.io/arabic-writing-skill/">docs</a></td>
</tr>
<tr>
<td><strong>نحو وإعراب</strong></td>
<td>ضبط الجملة وتصحيح الأخطاء النحوية</td>
<td><a href="https://specailm5.github.io/arabic-grammar-skill/">docs</a></td>
</tr>
<tr>
<td><strong>تحرير</strong></td>
<td>مراجعة نهائية للأسلوب والبنية قبل التسليم</td>
<td><a href="https://specailm5.github.io/arabic-editing-skill/">docs</a></td>
</tr>
<tr>
<td><strong>بلاغة</strong></td>
<td>تحليل الصورة وصناعتها ونقدها</td>
<td><a href="https://specailm5.github.io/arabic-balagha-skill/">docs</a></td>
</tr>
<tr>
<td><strong>قصة</strong></td>
<td>بناء القصة وشخصياتها ونهايتها</td>
<td><a href="https://specailm5.github.io/arabic-story-skill/">docs</a></td>
</tr>
<tr>
<td><strong>سيناريو</strong></td>
<td>مشاهد وحوار لفيلم أو مسلسل أو مسرح</td>
<td><a href="https://specailm5.github.io/arabic-screenwriting-skill/">docs</a></td>
</tr>
<tr>
<td><strong>حكايات أطفال</strong></td>
<td>حكاية مناسبة لعمر الطفل وجمهوره</td>
<td><a href="https://specailm5.github.io/arabic-children-story-skill/">docs</a></td>
</tr>
<tr>
<td><strong>مقال</strong></td>
<td>مقال رأي أو عمود أو خاطرة</td>
<td><a href="https://specailm5.github.io/arabic-essay-skill/">docs</a></td>
</tr>
<tr>
<td><strong>بحث</strong></td>
<td>سؤال وفجوة وخطة وتوثيق أكاديمي</td>
<td><a href="https://specailm5.github.io/arabic-academic-skill/">docs</a></td>
</tr>
<tr>
<td><strong>ترجمة</strong></td>
<td>ترجمة أمينة تحافظ على الأسلوب</td>
<td><a href="https://specailm5.github.io/arabic-tarjama-skill/">docs</a></td>
</tr>
<tr>
<td><strong>خطبة</strong></td>
<td>خطبتان على أصولهما، وفقه المذاهب، ونصوص متحققة</td>
<td><a href="https://specailm5.github.io/arabic-khutba-skill/">docs</a></td>
</tr>
<tr>
<td><strong>إعلام</strong></td>
<td>خبر وتقرير وتحقيق بتحقق من المصادر</td>
<td><a href="https://specailm5.github.io/arabic-media-skill/">docs</a></td>
</tr>
<tr>
<td><strong>إعلان</strong></td>
<td>نص تسويقي لجمهوره ووسيطه</td>
<td><a href="https://specailm5.github.io/arabic-copywriting-skill/">docs</a></td>
</tr>
</tbody>
</table>
<br clear="all">

**قادم:** الشعر، الرواية الطويلة، المسرح، الحكايات المصورة والتفاعلية.

---

## 🧩 أمثلة

<table dir="rtl" align="right">
<thead>
<tr>
<th align="right">تكتب</th>
<th align="right">ما يحدث</th>
</tr>
</thead>
<tbody>
<tr>
<td>«اكتب قصة قصيرة عن الغربة»</td>
<td>يسأل عن الطول والنهاية، ثم يكتب القصة</td>
</tr>
<tr>
<td>«اكتب حكاية للأطفال عن الصدق»</td>
<td>يسأل عن العمر، ثم يكتب الحكاية</td>
</tr>
<tr>
<td>«اكتب مقالاً عن التعليم»</td>
<td>يسأل عن نوع المقال، ثم يكتبه</td>
</tr>
<tr>
<td>«اكتب بحثاً عن الذكاء الاصطناعي»</td>
<td>يسأل عن المستوى والتوثيق، ثم يبني الخطة</td>
</tr>
<tr>
<td>«اكتب خطبة جمعة عن الصبر»</td>
<td>يسأل عن المذهب، ثم يكتب الخطبتين</td>
</tr>
<tr>
<td>«ترجم هذا المقال»</td>
<td>يسأل عن الاتجاه والمجال، ثم يترجم</td>
</tr>
<tr>
<td>«صحح النحو في هذا النص»</td>
<td>يعيد النص مضبوطاً ويبيّن الأخطاء</td>
</tr>
<tr>
<td>«حرّر هذا النص»</td>
<td>يراجع الأسلوب والبنية قبل التسليم</td>
</tr>
<tr>
<td>«أعد صياغته بأسلوب أفضل»</td>
<td>يعيد الصياغة بأسلوب عربي طبيعي</td>
</tr>
<tr>
<td>«حلّل الاستعارة في هذا البيت»</td>
<td>يشرح الصورة ووجه الشبه وأثرها</td>
</tr>
<tr>
<td>«اكتب إعلاناً لتطبيق ميزانية»</td>
<td>يسأل عن الجمهور والدليل، ثم يكتب</td>
</tr>
</tbody>
</table>
<br clear="all">

---

## 📚 عن المشروع

قلم مستودع مهارات: كل نوع حزمة مستقلة، وسجلّها الكامل — الروابط وأوامر التثبيت وما تحتاجه كل حزمة — في [`references/registry.json`](skills/qalam/references/registry.json). لمن يريد الجانب التقني: [`SKILL.md`](skills/qalam/SKILL.md) و[`routing_rules.md`](skills/qalam/references/routing_rules.md).

---

## 🤝 المساهمة

نرحب بالمساهمات التي تحسّن الأمثلة أو التوصيف أو التوثيق. اقرأ [CONTRIBUTING.md](CONTRIBUTING.md) قبل فتح طلب سحب، والتزم بـ[قواعد السلوك](CODE_OF_CONDUCT.md).

## 🛡️ الأمان

إن وجدت مشكلة أمنية، فلا تفتح قضية عامة؛ راجع [SECURITY.md](SECURITY.md).

## 📄 سجل التغييرات

راجع [CHANGELOG.md](CHANGELOG.md).

## 📬 الدعم

للأسئلة والاقتراحات: [افتح قضية](https://github.com/specailm5/qalam/issues).

---

## 📜 الترخيص

هذه المهارة مفتوحة المصدر تحت رخصة [MIT](LICENSE).
