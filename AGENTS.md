# Code Taste

Preferences for this codebase. Follow existing patterns first. Apply these unless a specific case has a stronger reason.

## General

- Keep changes small and focused.
- Look for existing patterns before adding new ones.
- Reuse or extend existing components/helpers when possible.
- Create abstractions only when similar patterns repeat.

## Python

- No `_` prefix for helper functions — they aren't truly private here and the prefix adds noise. Use plain `snake_case`.
- Keep functions/methods small (~10 lines when practical).
- Prefer OOP and keep logic close to the object it belongs to.
- Avoid comments that explain what the next line does.
- Add comments only for non-obvious reasons: constraints, workarounds, or important assumptions.
- Don't repeat docstrings in comments.

## Vue / TypeScript

- Use existing frappe-ui components before creating custom UI
- Keep page templates small.
- Move large/repeated UI pieces into feature-specific `.vue` components.
- Check for similar code before building something new. Extract common patterns when repetition appears.

## سياسة تحديث Press: التحديث في المكان أولًا
كل تحديث كود لتطبيق موجود على bench قائم يمر عبر In-place update في Press وفق [السياسة المركزية](https://github.com/bdcbiz/almadrasa-press-infra/blob/main/docs/ops/PRESS-UPDATE-POLICY.ar.md).
التفعيل مشروط بنجاح staging على bench-0005 ثم موقع إنتاجي واحد؛ حتى تنجح التجربتان يبقى البناء الكامل.
البناء الكامل للحالات غير المدعومة أو التي يمنعها التحفظ وفق السياسة؛ وتغييرات التبعيات تتطلب staging أولًا.
صنّف الفرق الكامل بين SHA المنشور والهدف، واحجز bench ومواقعه وموارده المشتركة في LIVE-WRITER؛ bench واحد في كل مرة.
قبل migrate: نسخة حديثة مع اختبار استرجاع معزول وفحص الأقفال؛ وثّق last-good image وdigest واحمِها من GC.
تحقق من نجاح Agent Job وتطابق hashes وصحة العمليات وsmoke tests؛ عند الفشل استعد وتحقق من قاعدة البيانات ولا تعاود قبل المراجعة.
ممنوع تعديل الكود يدويًا داخل الحاويات؛ كل دمج عبر PR ومراجعة مستقلة، بلا force-push أو --no-verify أو أسرار.
