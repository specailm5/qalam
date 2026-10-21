# مهارة توجيه المهارات العربية
### (Arabic Workflow / Intent Router Skill)

<p align="center">
  <a href="https://github.com/specailm5/arabic-workflow-skill/blob/master/LICENSE"><img alt="License" src="https://img.shields.io/github/license/specailm5/arabic-workflow-skill?style=flat-square"></a>
  <a href="https://github.com/specailm5/arabic-workflow-skill/commits/master"><img alt="Last commit" src="https://img.shields.io/github/last-commit/specailm5/arabic-workflow-skill?style=flat-square"></a>
  <a href="https://specailm5.github.io/arabic-workflow-skill/"><img alt="Docs" src="https://img.shields.io/badge/docs-live-brightgreen?style=flat-square"></a>
  <img alt="Agent Skills" src="https://img.shields.io/badge/Agent%20Skills-compatible-5B21B6?style=flat-square">
  <img alt="Meta skill" src="https://img.shields.io/badge/type-meta--skill-0F766E?style=flat-square">
</p>

**Arabic intent-router for AI agents** — loads first, reads the request, and selects the smallest correct set of Arabic skills: `«اكتب قصة للأطفال»` → `children-story` + `writing` + `grammar` + `editing`, not all thirteen. It contains the registry of every repository URL and install command. It does not write the content itself.

🔗 **الموقع المرجعي (السجل والتوجيه والأمثلة): [specailm5.github.io/arabic-workflow-skill](https://specailm5.github.io/arabic-workflow-skill/)**

> مهارة **ميتا** لنماذج الذكاء الاصطناعي والمحررات الذكية (Codex، Claude Code، Antigravity IDE، VS Code Agent Harness): تُحمَّل أولاً، تحدد نية المستخدم، ثم تختار المهارات وترتّب تحميلها. **خط الأساس:** `arabic-writing-skill` (نبذ العَرَنْجِيَّة) + `arabic-grammar-skill`، و**التمرير النهائي:** `arabic-editing-skill`.

---

## 📖 ما هي المهارة؟

ليست مهارة كتابة. هي **موجّه**. المشكلة التي تحلها:

- المنظومة فيها ١٣ مهارة، وتحميلها كلها يفسد الاختيار.
- الطلب الواحد قد يحتمل أكثر من جنس.
- بعض المهارات إلزامية (اللغة والنحو)، وبعضها لا يُحمَّل إلا عند الحاجة.
- المستخدم لا يعرف أسماء المهارات ولا روابطها.

فتُحمَّل هذه المهارة أولاً، وتخرج **بطاقة توجيه**:

```yaml
intent: short-story
primary: arabic-story-skill
supporting: []
baseline: [arabic-writing-skill, arabic-grammar-skill]
final_pass: arabic-editing-skill
order: [writing, grammar, story, editing]
missing: [length, audience]
cautions: ["حدث واحد، لا تقرير."]
```

**القاعدة:** مهارة أساسية واحدة + خط الأساس + التحرير. والمساندة بالحاجة فقط.

---

## ⚡ خط الأساس

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
<td><strong>إلزامية</strong></td>
<td>كل نص عربي — الأسلوب ونبذ العَرَنْجِيَّة</td>
</tr>
<tr>
<td><code>arabic-grammar-skill</code></td>
<td><strong>إلزامية</strong></td>
<td>كل نص عربي — النحو والإعراب</td>
</tr>
<tr>
<td><code>arabic-editing-skill</code></td>
<td><strong>تمرير نهائي</strong></td>
<td>قبل التسليم — إلا إذا طُلبت مسودة سريعة</td>
</tr>
</tbody>
</table>
<br clear="all">

---

## 🗂️ سجل المهارات

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
<td>أطفال/يافعين</td>
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

**المخطط لها:** الشعر، الرواية الطويلة، المسرح، القصص المصورة، القصص التفاعلية. لا تُحمَّل كأنها منشورة.

---

## 📂 بنية المستودع

<pre dir="rtl"><code>
arabic-workflow-skill/
│
├── skills/arabic-workflow-skill/          # المهارة (تركيب Agent Skills القياسي)
│   ├── SKILL.md                           # قواعد التوجيه فقط
│   ├── references/
│   │   ├── registry.json                  # سجل الآلة: الروابط والتثبيت والمحفزات
│   │   ├── skill_registry.md              # سجل بشري بكل الروابط
│   │   ├── routing_rules.md               # التعارض والترتيب
│   │   └── ambiguity.md                   # أسئلة فك الالتباس
│   └── examples/
│       ├── routing_cases.md               # عشرون حالة
│       └── multi_skill_requests.md        # الطلبات المركّبة
│
├── docs/                                  # الموقع المرجعي (GitHub Pages)
│
├── .agents/skills/arabic-workflow-skill/  # مسار Codex و Antigravity
│
└── .claude/skills/arabic-workflow-skill/  # مسار Claude Code
</code></pre>

---

## 🚀 التثبيت

### الطريقة الأسرع

```bash
npx skills add specailm5/arabic-workflow-skill -g -y
```

### مع خط الأساس

```bash
npx skills add specailm5/arabic-workflow-skill -g -y
npx skills add specailm5/arabic-writing-skill -g -y
npx skills add specailm5/arabic-grammar-skill -g -y
npx skills add specailm5/arabic-editing-skill -g -y
```

ثم ثبّت المهارة النوعية التي تحتاجها فقط:

```bash
npx skills add specailm5/arabic-story-skill -g -y
npx skills add specailm5/arabic-children-story-skill -g -y
npx skills add specailm5/arabic-essay-skill -g -y
```

### التثبيت اليدوي (Windows)

```powershell
$src = "skills\arabic-workflow-skill"

New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.claude\skills\arabic-workflow-skill"
Copy-Item -Recurse -Force "$src\*" "$env:USERPROFILE\.claude\skills\arabic-workflow-skill\"

New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.agents\skills\arabic-workflow-skill"
Copy-Item -Recurse -Force "$src\*" "$env:USERPROFILE\.agents\skills\arabic-workflow-skill\"
```

### التثبيت اليدوي (macOS / Linux)

```bash
src=skills/arabic-workflow-skill

mkdir -p ~/.claude/skills/arabic-workflow-skill
cp -r "$src/." ~/.claude/skills/arabic-workflow-skill/

mkdir -p ~/.agents/skills/arabic-workflow-skill
cp -r "$src/." ~/.agents/skills/arabic-workflow-skill/
```

### الاستخدام اليدوي

انسخ محتوى [`skills/arabic-workflow-skill/SKILL.md`](skills/arabic-workflow-skill/SKILL.md) إلى **التعليمات المخصصة** أو **System Prompt**، وثبّت خط الأساس.

---

## 🧭 كيف يقرر؟

<table dir="rtl" align="right">
<thead>
<tr>
<th align="right">الإشارة</th>
<th align="right">السؤال</th>
<th align="right">أثرها</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>النوع</strong></td>
<td>قصة، مقال، خبر، خطبة؟</td>
<td>يحدد المهارة الأساسية</td>
</tr>
<tr>
<td><strong>المخرج</strong></td>
<td>مسودة، نقد، تحرير، ترجمة؟</td>
<td>يحدد هل الأساسية نوع أم تحرير</td>
</tr>
<tr>
<td><strong>الجمهور</strong></td>
<td>أطفال، أكاديميون، عام؟</td>
<td>يغيّر المهارة</td>
</tr>
<tr>
<td><strong>الوسيط</strong></td>
<td>مطبوع، فيلم، مسرح، سوشيال؟</td>
<td>يغيّر الصيغة</td>
</tr>
<tr>
<td><strong>اللغة</strong></td>
<td>عربية، إنجليزية، ثنائية؟</td>
<td>يحدد الترجمة</td>
</tr>
<tr>
<td><strong>الخطر</strong></td>
<td>دين، طب، قانون، أطفال؟</td>
<td>يفرض أسئلة وتحذيرات</td>
</tr>
</tbody>
</table>
<br clear="all">

### ترتيب التحميل

<pre dir="rtl"><code>
① arabic-writing-skill      (خط الأساس اللغوي)
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
<td>«اكتب قصة للأطفال عن الصدق»</td>
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
<td>«اكتب سيناريو مشهد»</td>
<td><code>arabic-screenwriting-skill</code></td>
<td>اسأل فيلم/مسلسل</td>
</tr>
<tr>
<td>«ترجم هذا المقال»</td>
<td><code>arabic-tarjama-skill</code></td>
<td>اسأل الاتجاه</td>
</tr>
<tr>
<td>«اكتب خطبة جمعة»</td>
<td><code>arabic-khutba-skill</code></td>
<td><strong>اسأل المذهب أولاً</strong></td>
</tr>
<tr>
<td>«اكتب خبراً عن حادث»</td>
<td><code>arabic-media-skill</code></td>
<td>تحقق من المصادر</td>
</tr>
<tr>
<td>«اكتب إعلاناً لتطبيق»</td>
<td><code>arabic-copywriting-skill</code></td>
<td>اسأل الجمهور والدليل</td>
</tr>
<tr>
<td>«حلّل هذه الاستعارة»</td>
<td><code>arabic-balagha-skill</code></td>
<td>—</td>
</tr>
</tbody>
</table>
<br clear="all">

---

## 🛠️ إضافة مهارة جديدة

1. أضف سجلاً في `references/registry.json`.
2. أضف صفاً في `references/skill_registry.md`.
3. أضف صفاً في جدول `SKILL.md`.
4. اختبر خمس حالات توجيه.
5. ارفع `version` في frontmatter.

**قاعدة:** لا تُضف مهارة بلا `repo_url` و`raw` و`install`. والمخطط لها تُسجَّل في `planned` بلا رابط.

---

## ⚠️ الحدود

- **لا تكتب المحتوى**؛ التوجيه ليس إنشاءً.
- **لا تفتي**؛ الخطبة تُعرض ولا تُفتي.
- **لا تختلق مصادر** أو وقائع.
- **لا تُقدّم استشارة طبية/قانونية.**
- **لا تُحمِّل مهارة غير مسجّلة.**
- **لا تَعِد بمهارة مخطط لها** كأنها منشورة.
- المستخدم مسؤول عن مراجعة الناتج النهائي.

---

## 📚 ملاحظة المصادر

هذه **مهارة ميتا**، وليست مهارة كتابة. لا تُعلِّم جنساً أدبياً ولا نحواً ولا بلاغة، بل تُوجِّه إلى من يُعلِّم. لذلك لا تنطبق عليها قاعدة «٢–٤ كتب»؛ سجلّها هو `references/registry.json`، ومصادرها هي مهارات المنظومة نفسها.

---

## 🤝 المساهمة

نرحب بالمساهمات التي تحسّن السجل أو قواعد التوجيه. اقرأ [CONTRIBUTING.md](CONTRIBUTING.md) قبل فتح طلب سحب، والتزم بـ[قواعد السلوك](CODE_OF_CONDUCT.md).

## 🛡️ الأمان

إن وجدت مشكلة أمنية، فلا تفتح قضية عامة؛ راجع [SECURITY.md](SECURITY.md).

## 📄 سجل التغييرات

راجع [CHANGELOG.md](CHANGELOG.md).

## 📬 الدعم

للأسئلة والاقتراحات: [افتح قضية](https://github.com/specailm5/arabic-workflow-skill/issues).

---

## 📜 الترخيص

هذه المهارة مفتوحة المصدر تحت رخصة [MIT](LICENSE).
