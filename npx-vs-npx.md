Original article: https://www.freecodecamp.org/news/npm-vs-npx-whats-the-difference/

# ما هو الفرق بين npm و npx؟

## أذا استخدمت [Node.js](https://nodejs.org/), فبالتأكيد أنك استخدمت npm.

يكون **npm** مدير إلى `dependency/package`, تحصل عليه تلقائًا عند تركيب Node.js.

أحياناً ترغب في المتالعة على حزمة محدد وتجربة بعض الأوامر. لكنك لا تستطيع القيام بالتجربة بدون تركيب التبعيات في ملف `node_modules` المحلي.

هنا يمكن استخدام **npx** لفعل ذلك

في هذا المقال, ستتعرف على الفرق بين **npm** و **npx**, وستعلم كيفية استخدامهم بشكل حسن.

أذا فضلت مشاهدة فيديو, يمكنك مشاهدة هذا الفيديو بالأنجليزية

<video autosize="true">
<source src="https://www.youtube.com/watch?v=fSHWc8RTJug&t=3s">
</video>

## **إدارة حزمة بواسطة npm**

يتكون npm من جزئين. أولاً, يكون الجزء الاول مستودع في شبكة الألكترونية, تستخدم للنشر مشاريع Node.js مفتوحة المصدرة.
 ولكن لا تريد تركيبهم.

 
يتكون الجزء الثاني من اداه تسمي (CLI) مصدرة للأوامر التي تساعد في تركيب حزمة ولكن لا تريد تركيبهم.

م وادارة نسخ الأصدار و التبعيات. يوجد مئات الألاف المكتبات والطبيقات من Node.js ويضيف المزيد يومياً في npm.

لا يُفعيل npm الحزم تلقائًا. عندما ترغب بتفعيل الحزمة باستخدام npm, يجب عليك تحديد تلك الحزمة في ملف `package.json`.

عند تركيب الملفات قابلة التنفيذ بواسطة حزم npm, ينشئ npm نوعين من الروابط:

- تنشاء روابط التركيبات **المحلية** في مستند `./node_modules/.bin/`
- تنشاء روابط التركيبات **العالمية** في مستند `bin/` (مثل: `/user/local/bin` في نظام Linux, أو `%AppData%/npm` في نظام Windows)

لتنفيذ الحزمة بواسطة npm, يجب كتابة المسار المحلي, هكذا:

```pwsh
./node_modules/.bin/your-package
```

أو يمكنك تفعيل الحزم المركبة محلياً من خلال أضافة الحزمة إلى ملف `package.json` في مقطع `scripts`, مثل:

```json
{
  "name": "your-application",
  "version": "1.0.0",
  "scripts": {
    "your-package": "your-package"
  }
}
```

ثم تفعيل البرنامج باستخدام `npm run`:

```pwsh
npm run your-package
```

لحسن الحظ, يسهل npx سير العملية.

## **تفعيل الحزمة بواسطة npx**

منذ نسخة [5.2.0](https://github.com/npm/npm/releases/tag/v5.2.0), يتركب npx مع npx. لذلك من المتوقع وجودهما عند تركيب Node.js في الأيام الحالية.

يتكون npx من اداه (CLI) مصدرة للأوامر التي تهدف لتسهيل تركي ولكن لا تريد تركيبهم.

ب الحزم وادارة نسخ الأصدار في تسجيل npm.

يمكنك تفعيل أي ملف قابل التنفيذ في Node.js, الذي يمكن تركيبه من خلال npm.

أكتب الأمر التالي لتأكد من وجود npx في نظامك.

```bash
which npx
```

يمكنك تركيبه أذا لم تجده:

```bash
npm install -g npx
```

عندما تتيقن من تركيبه, يمكن متابعة المقال لتّعرف على عدة استخدمات مفيدا جداً له.

## **تفعيل حزمة مركبة بسهولة**

أن كنت ترغب في تركيب الحزمة السابقة من خلال npx, أكتب الأتي:

```bash
npx your-package
```

سوف يتحقق npm من وجود `<command>` أو `<package>` في `$PATH`, أو في الملفات الثنائية في مشرعك المحلي, يتم تفعيله عند وجوده.

## **تفعيل حزم التي لم يتم تركيبها من قبل**

من الميزات npx الرئيسي, القدرة علي تفعيل حزمة لم يتم التركيبه مسبقاً.

يمكنك تجربة هذا بكتابة هذا:

```bash
npx cowsay wow
```

![npm-vs-npx](https://i2.wp.com/neutrondev.com/wp-content/uploads/2020/01/npx-cowsay-wow-npm-vs-npx.jpg)

هذا رائع لأنك قد ترغب باستخدام بعض أدوات مصدرة للأوامر ولكن لا تريد تركيبهم, وتقلل من تلوث المتغيرات العالمية التي يمكن تغيرها عند التركيب.

### **تفعيل التعليمات من GitHub مباشرتاً**

![execute-gist-scripts-with-npx](https://www.freecodecamp.org/news/content/images/2020/01/execute-gist-scripts-with-npx.jpg)

يمكنك استخدام npx لتعامل مع المستودعات GitHub. يتكون التعليمات الأساسية من ملف JavaScript أساسي و `package.json`. كل ما تحتاجه فعله بعد أنشاء الملفات, هو تفعيل رابط المستودع بواسطة كما يوضح في الصورة.

يمكنك تحري التعليمات المستخدمة في المثال [هنا](https://gist.github.com/Tynael/0861d31ea17796c9a5b4a0162eb3c1e8).

يجب التأكد من التعليمات قبل تفعيلها, لتجنب مشاكل خطرة التي تحدث عند تفعيل تعليمات خبيث.

### **أختبار نسخ مختلفة من الحزمة**

يجعل npx من السهل أختبار نسخ مختلفة من حزمة أو وحده نمطيه من  Node.js. لأختبار هذه الميزة المتازة, سوف تركب حزمة `create-react-app` محلياً وتجربة نسخة.

لمعرفة نسخة الحزمة قبل تركيبها, يمكنك استخدام علامة Dist:

```pwsh
npm v create-react-app
```

![create-react-app-dist-tags](https://www.freecodecamp.org/news/content/images/2020/01/create-react-app-dist-tags.jpg)

استخدم npx لتركيب نسخة `next` بواسطة علامة dist في حزمة `create-react-app`, التي ستنشئ تطبيق داخل بيئة للأختبارات.

```pwsh
npx create-react-app@next sandbox
```

سوف يركب npx نسخة من حزمة `create-react-app` مؤقتاً, ثم يفعل التطبيق وتركيب تبيعاتها.

يمكن تنقل ألى التطبيق عند التركيب, مثل: 

```pwsh
cd sandbox
```

ثم بدء أدارتها عن طريق:

```pwsh
npm start
```

![create-react-app-npx-next-version](https://www.freecodecamp.org/news/content/images/2020/01/create-react-app-npx-next-version.jpg)

سوف يفتح المتصفح نسخة next من حزمة تطبيق React تلقائًا.

![react-app](https://www.freecodecamp.org/news/content/images/2020/01/react-app.jpg)

## **ملخص**

يساعد npx على تجنب تركيب نسخ وتبيعاتها والحزم بشكل دائم.

يوفر npx طريقة لتفعيل حزم, وأوامر, ووحدات, ومستودعات بسهولة.

كتب [Carol-Theodor Pelu](https://www.freecodecamp.org/news/author/carol-theodor-pelu/) المقال الأصلي, يمكنك متابعته في [Twitter](https://twitter.com/pelu_carol) و [Facebook](https://www.facebook.com/neutrondevcom), أو قراءة مقالته أخري بالأنجليزية [هنا](https://neutrondev.com/npm-vs-npx-whats-the-difference/).
