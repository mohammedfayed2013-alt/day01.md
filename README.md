# day01.md
# Day 01 — مواقف غلط فيها الموديل

> املأ كل موقف بعد ما تجرب فعليًا مع أي موديل AI (ChatGPT / Claude / Gemini...).
> لازم 5 مواقف من 5 فئات مختلفة على الأقل 3 فئات، والأسئلة تبقى مرتبطة بـ Laravel / Next.js / Flutter / MySQL / cPanel (مش أسئلة عامة).

---

## الموقف 1

**الفئة:** (مثال: Laravel Eloquent / Next.js Routing / Flutter Widgets / MySQL Query / cPanel Config)

**الـ prompt:**الفئة: Next.js Routing
الـ prompt: "اشرحلي إزاي أستخدم intercepting routes في Next.js مع أمثلة على (.) و(..) و(...)"
الرد (الجزء الغلط): مثال هيكل الفولدرات لاستخدام (..) — @modal جوه [id]/ باسم (..)page.tsx، وعدم ذكر (..)(..) كصيغة موجودة خالص
الغلط بالتحديد: 1) الـ @modal المفروض يكون بنفس مستوى الـ segment اللي عايز تعترضه مش جوه segment فرعي منه، والاسم المفروض يشاور على الـ segment المستهدف (زي (..)[id]) مش "page.tsx". 2) صيغة (..)(..) لمسافة مستويين فوق مش موجودة في شرح الموديل خالص
الدليل: nextjs.org/docs/app/api-reference/file-conventions/intercepting-routes — بيوضح إن (..)(..) بتطابق segments مستويين فوق، وإن الـ @modal بيتحسب كـ slot مش segment فالعد بيتجاهله
السبب المحتمل: خلط بين الـ file-system nesting (المستويات الفعلية في الفولدرات) وبين الـ route segment counting (اللي بيتجاهل الـ @slot folders)
```
## الموقف 2

**الفئة:**الموقف: مصدر شرح NextJS اقترح إن @modal prefix هو اللي بيعمل الـ interception
الـ prompt: "اشرحلي إزاي أعمل intercepting routes في Next.js وإيه صيغة الـ Link"
الرد (الجزء الغلط): "استخدم @ prefix عشان تعمل intercepting route، والينك هيبقى href='/dashboard.(sidebar)'"
الغلط بالتحديد: الـ @ prefix بيعرّف Parallel Route slot مش intercepting route، والـ interception الفعلي بيحصل بصيغة (.)  (..)  (...) في اسم الفولدر، ومفيش صيغة href='/path.(slot)' في التوثيق الرسمي أصلاً
الدليل: رابط توثيق — nextjs.org/docs/app/api-reference/file-conventions/intercepting-routes
السبب المحتمل: خلط بين مفهومين متشابهين (Parallel Routes و Intercepting Routes) لأنهم بيتستخدموا مع بعض غالبًا في نفس المثال (المودال)
