original article: https://www.freecodecamp.org/news/git-checkout-remote-branch-tutorial/

original author: https://www.freecodecamp.org/news/author/dillionmegida/

---

# طريقة عمل Git Checkout Remote Branch

يكون Git أداة لتحكم الذي تسمح لك بصيانة ومشاهدة نسخ إصدارات مختلفة من تطبيقك. عند إضافة مِيزة جديدة تضر تطبيقك, يمكنك التراجع عن ذلك بواسطة التراجع إلى نسخة إصدار سابقة بواسطة Git.

بالإضافة ألى التحكم بنسخة الإصدار, يسمح Git بالعمل في بيئات عدّة في الوقت ذاته. تعني بيئات عدّة **branches** في هذا السياق.

## لماذا تحتاج branches

عند تعاملك مع Git, سوف تملك بيئة (branch) أساسية تسمى (master أو main). تحمل تلك البيئة التعليمات البرمجية المنشرة عندما يكون تطبيقك مُعدّ للإنتاج.

عندما ترغب بتحديث تطبيقك, يمكنك إضافة متغيرات (commits) ألى تلك branch. يبدو هذا كأمر بسيط أذا كانت التغيرات ليست مهمة, لكن فعل ذلك مع التغيرات الكبيرة غير مثالي. ولذلك يستخدم branches أخرى.

لإنشاء واستخدام branch جديد, أستخدم الأمر الأتي في terminal في مِلَفّ مشروعك:

```pwsh
# create a new branch
git branch branch-name
# change environment to the new branch
git checkout branch-name
```

يمكنك أنشاء متغيرات جديدة في تلك branch الجديدة. عندما تنتهي من ذلك, يمكنك دمجهم مع branch الأساسية.

من ميزات branches, السماح للعديد من المطورين العمل في نفس المشروع بشكل متزامن. أذا لديك خبرة مع مشروع  يطوره العديد من المطورين, فأنك تعرف كيف يمكن أن يكون الوضع كارثي. يتغير المشروع بكثرة مع كل تحسين يقوم بيه مطور, وهذا ينتهي بنزاع عند الدمج في أغلب الأحوال.

مع Git, يمكن للكل مطور العمل في branches مختلفة, وبالطبع يمكنك أنتقال إلى branch (بيئة خاصة بك) أيضا.

## ماذا تعني Git Checkout Remote Branch

عندما تبدأ مشروعك مع Git, حصل على بيئتين: بيئة محلية تسمى master branch (التي توجد في جهازك الحاسوب), وبيئة ألنائي remote branch (التي توجد في منصة تدعم Git مثل GitHub).

يمكنك إرسال التغيرات من البيئة المحالية (local master branch) إلى بيئة نائي (remote master branch) واستلام تغيرات من البيئة ألنائي.

عند أنشاء بيئة محلية, تكون البيئة محلية فقط, ألا عند إرسالها إلى GitHub حيث تصبح بيئة نائي أيضا. تبدو كهذا المثال:

```pwsh
# create a new branch
git branch new-branch
# change environment to the new branch
git checkout new-branch
# create a change
touch new-file.js
# commit the change
git add .
git commit -m "add new file"
# push to a new branch
git push --set-upstream origin new-branch
```

من المثال السابق, تصبح `origin new-branch` بيئة نائي. يمكن أن تكون لاحظت, ننشئ البيئة الجديدة ونضيف تغير أليها قبل إرسالها ألى البيئة النائي الجديدة.

ولكن ماذا أذا البيئة النائي موجودة فعلًا, وترغب إلى أستلام البيئة وكل المتغيرات في البيئة المحالية؟

## كيف استخدام Git Checkout Remote Branch

لنفترض وجود بيئة نائي أنشأت بواسطة مطور أخر, وترغب باستلام تلك البيئة, هنا كيفية عمل ذلك:

### 1- جلب كل Remote Branches

```pwsh
git fetch origin
```

يقوم الأمر بجلب جميع البيئات ألنائي من repository. يكون `origin` نوع ما تستهدفه, لذلك أذا رغبت بجلب بيئة نوعها `upstream`, تستخدم `git fetch upstream`.

### 2- حدد قائمة البيئات القابلة يمكن فحصها

لتتيقن البيئات القابلة للفحص, أستخدم التالي: 

```pwsh
git branch -a
```

ينتج من هذه قائمة من بيئات القابلة للفحص. ستجد البيئات ألنائي يبدئها `remotes/origin`.

### 3- أستلام المتغيرات من بيئة نائي

لاحظ لا يمكنك تغير بشكل مقصود على بيئة نائي, لذلك تحتاج إلى نسخ تلك البيئة. لنفترض أنك ترغب بنسخ بيئة تسمى `fix-failing-tests`, يمكنك فعل ذلك بهذه الطريقة:

```pwsh
git checkout -b fix-failing-tests origin/fix-failing-tests
```

سوف يفعل هذا الأتي:

- تنشئ بيئة جديدة تسمى `fix-failing-tests`
- تفحص (`checkout`) البيئة
- تستلم المتغيرات من بيئة `origin/fix-failing-tests`.

لديك ألأن نسخة من البيئة ألنائي, ويمكنك إرسال متغيرات أليها, مثل: 

```pwsh
touch new-file.js
git add .
git commit -m "add new file"
git push
```

سوف يرسل هذا المتغيرات إلى `origin/fix-failing-tests`. لا نحتاج تحديد أين نرسل المتغيرات مثل (`git push origin fix-failing-tests`), لأن Git يحدد مسار البيئة المحلية إلى البيئة ألنائي تلقائياً 


## ملخص

تجعل git branches من السهل التعاون خلال تطوير التطبيق.

مع branches, يمكن لمطورين العمل بسهولة في مقاطع مختلفة من البيئة بشكل متزامن.

مع checkout remote branch, يجعل التعاون سلس بين المطورين لأن من ممكن نسخ البيئات ألنائي في نظامك المحلي, وتغير التطبيق, وإرسال ألى البيئات ألنائي.

كتب المقال الأصلي بواسطة [Dillion Megida](https://www.freecodecamp.org/news/author/dillionmegida/).
