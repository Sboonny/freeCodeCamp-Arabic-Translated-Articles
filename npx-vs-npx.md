Original article: https://www.freecodecamp.org/news/npm-vs-npx-whats-the-difference/

Original Author: https://www.freecodecamp.org/news/author/carol-theodor-pelu/

# ما هو الفرق بين npm و npx؟

## أذا استخدمت [Node.js](https://nodejs.org/), فبالتأكيد أنك استخدمت npm.

يكون **npm** مدير إلى dependency/package, تحصل عليه تلقائًا عند تثبيت Node.js.

أحياناً ترغب في المتالعة على حزمة محدد وتجربة بعض الأوامر. لكنك لا تستطيع القيام بالتجربة بدون تثبيت التبعيات في ملف `node_modules` ا9لمحلي.

هنا يمكن أستخدام **npx** لفعل ذلك

في هذا المقال, ستتعرف على الفرق بين **npm** و **npx**, وستعلم كيفية استخدامهم بشكل حسن.

أذا فضلت مشاهدة فيديو, يمكنك مشاهدة هذا الفيديو بالأنجليزية

***remeber to embed the video***

https://www.youtube.com/watch?v=fSHWc8RTJug&t=3s

**إدارة حزمة بواسطة npm**

يتكون npm من جزئين. أولاً, يكون الجزء الاول مستودع في شبكة الألكترونية, تستخدم للنشر مشاريع Node.js مفتوحة المصدر.

يتكون الجزء الثاني من اداه تسمي (CLI) مصدر الأوامر التي تساعد في تثبيت حزم وادارة نسخ الأصدار و التبعيات. يوجد مئات الألاف المكتبات والطبيقات من Node.js ويضيف المزيد يومياً في npm.

