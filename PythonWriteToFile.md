https://www.freecodecamp.org/news/python-write-to-file-open-read-append-and-other-file-handling-functions-explained/

---

Arabic Translation

# كاتبة مِلَفّ باستخدام وظائف في Python- مثل Open, وRead, وAppend, ومثيل ذلك من Functions التي تتلاعب بالمِلَفّ

![Python-File-Handling-1](https://user-images.githubusercontent.com/88248797/185757885-f94ac99a-36bb-4e1e-a827-7d96f95c984c.png)

# مرحباً

أذا ترغب في تعلم المهارة المهمة وهي كيفية التعامل مع الملفات بواسطة Python, فإن هذا المقال من أجلك.

**ستّعلم في هذا المقال:**

- كيفية فتح مِلَفّ.
- كيفية قراءة مِلَفّ.
- كيفية أنشاء مِلَفّ.
- كيفية تعديل مِلَفّ.
- كيفية غلق مِلَفّ.
- كيفية فتح مِلَفّات من عدة عمليات.
- كيفية التعامل مع مِلَفّ object methods.
- كيفية حذف المِلَفّات.
- كيفية العمل مع منظمي المحتوى وما أهميتهم.
- بالإضافة إلى المزيد.

## 🔹 التعامل مع المِلَفّات: تشكيل أساسي

واحد من أهم functions التي ستحتاج إلى أستخدمها في المِلَفّات مع Python هي `open()`, وهي Function مدمجة داخلياً الذي يفتح المِلَفّ وتسمح لبرنامجك أستعمال والتعامل مع المِلَفّ.

**هذا هو التشكيل الأساسي**

![وظيفة Python](https://user-images.githubusercontent.com/88248797/185758931-116978ce-0633-4ce6-a2d6-f1aaaa327766.png)

**💡 تلميح:** هتين arguments من الأكثر شيوعيٍ فى هذا function. يوجد ست arguments أختيارين أخري. لتعلم المزيد عنهم, يمكنك قراءة [هذا المقال](https://docs.python.org/3/library/functions.html#open) في المستنادات.

### أول Parameter: المِلَفّ

تكون أول حِجَّة من وظيفة `open()` هي **`file`**, وتكون الطرق مطلقة أو نسبية للمِلَفّ الذي ترغب باستخدامه.

في العادة ستستخدم الطريق النسبي, لأشاره إلي إين يوجد المِلَفّ بالنسبة إلى المِلَفّ البرنامَج (Python file) الذي يستخدم وظيفة `open()`.

تكون طريقة أستخدام هذه الوظيفة, مثل:

```py
open("names.txt") # The relative path is "names.txt"
```

يحتوي على أسم المِلَفّ فقط. يمكن أستخدام ذلك عندما يحاول Python script المِلَفّ فتح نفس الدليل أو مستند, مثل:

 ![مِلَفّ و دليل](https://user-images.githubusercontent.com/88248797/186231796-d686be60-a3a5-4835-b215-03a08f4f7789.png)

ولكن عندما أدخال المِلَفّ داخل مستند, مثل:

![مِلَفّ في مستند](https://user-images.githubusercontent.com/88248797/186232255-e35fc4fe-c36f-41e0-9800-a631aca3af8f.png)

ثم تحتاج إلى أستخدام طريق محدد لأخبار الوظيفة, إن المِلَفّ داخل المستند.

سيكون الطريق مثل: 

```py
open("data/names.txt")
```

لاحظ إنك تكتب أولاً `data/` (اسم المستند يليه علامة `/`), ثم `names.txt` (اسم المِلَفّ مع ملحق).

**💡 تلميح:** تكون الثلاث أحرف `.txt` (الذي يتبعوا النقطة في `names.txt`) ملحق للمِلَفّ, أو نوعه. في هذه الحالة, تشير `.txt` إن المِلَفّ يكون نصي.


**الحَجَّة الثانية: الطريقة**

إن تكون الحَجَّة الثانية من وظيفة `open()` هو `mode`, مقطع نصي (string) بحرف واحد. يُملي الحرف الواحد Python ما تنوي فعله في المِلَفّ باستخدام برنامجك.

تكون الطرق المتاحة:
- قراءة (`"r"`) Read.
- ألحق (`"a"`) Append. 
- كتابة (`"w"`) Write. 
- إنشاء (`"x"`) Create.

يمكنك الاختيار فتح المِلَفّ في هيئة:

- هيئة نصية (`"t"`) Text mode
- هيئة ثنائي (`"b"`) Binary mode

لاستخدام الهيئتين, يجب إن تضف أحرافهم إلي الطريقة الأساسية (main mode). مثل: يعني `"wb"` انك ترغب بكتابة على هيئة ثنائي (Binary mode).

**💡 تلميح:** تكون الطرق والهيئات ألافتراضية هن قراءة (`"r"`) وكتابة (`"t"`), بمعنى "مفتوح لقراءة النص (open for reading text)" بشكل (`"rt"`), لذلك لا تحتج تحديدهم في طريقة `open()` عند الرغبة باستخدامهم, لأن يتم تحديدهم أفتراضياً. يمكنك كتابة `open(<file>)` بّساطة.

#### **لماذا أستخدام الطرق؟**

من المنطقي إن يمنح Python أذن محدد بالاستناد على ما تنوي فعله بالمِلَفّ. لا ترد أن يفعل Python شئياً لا تكن تّوقعه, لذلك أنشئت الطرق (modes).

تخيل هذا - أردت البرنامَج أن يقراْ المِلَفّ فقط, لكن يمكن للبرنامج تعديله أيضاً بشكل غير متوقع, فإن ذلك يضع المِلَفّ في خطر وينتج أضرار محتملة.

## 🔸 كيفية قراءة المِلَفّ

بعد معرفة أكثر عن الحجج الذي يقبلها وظيفة `open()`, ستّعلم كيفية فتح المِلَفّ و تخزينه في متغير (var) لتستخدمه في برنامجك.

![image-41](https://user-images.githubusercontent.com/88248797/187084038-5789b14c-d2d0-4d1d-be84-6a6dc384bbe6.png)

تعيين القيمة الناتجة إلى المتغير ببساطة, مثل:

```py
names_file = open("data/names.txt", "r")
```

ربما تتساءل ما نوع القيمة الناتجة من `open()`؟ أنه يكون **كائن مِلَفّ (file object)**.

## **كائنات المِلَفّ**

وفقاً [لتوثيق Python](https://docs.python.org/3/glossary.html#term-file-object), يكون كائن المِلَفّ كالتالي:

 > An object exposing a file-oriented API (with methods such as read() or write()) to an underlying resource.

هذا يخبرك إن كائن المِلَفّ يكون كائن يسمح بالتعامل والتفاعل مع مِلَفّات موجودة في برنامَج Python.

يملك كائنات المِلَفّ خصائص, مثل:
- **name**: أسم المِلَفّ.
- **mode**: طريقة فتح المِلَفّ.
- **close**: تكون علي هيئتين هم:

الهيئة الأولى هي `True` وتدل إن المِلَفّ مغلق.
الهيئة الثانية هي `False`, تدل إن المِلَفّ مفتوح.

![image-57](https://user-images.githubusercontent.com/88248797/187186804-1c52b225-67dd-49fc-b0b1-cc61b01a5c39.png)


مثل: 

```py
f = open("data/names.txt", "a")
print(f.mode) # Output: "a"
```

وبذلك قد فتح مِلَفّ `name.txt`.

### **طريق قرائة محتوي المِلَفّ**

ستّعلم ما تحتاجه من أول طريقة مسمى `read()`, التي **تنتج محتوي المِلَفّ بالكامل على هيئة مقطع نصي**.

![image-11](https://user-images.githubusercontent.com/88248797/187187814-99700f67-9d09-476d-9bde-e997e81c345a.png)

مثل

```py
f = open("data/names.txt")
print(f.read())
```

تنتج محتوي مِلَفّ `names.txt`:

```md
Nora
Gino
Timmy
William
```

يمكنك أستخدام وظيفة `type()` لتأكيد أن قيمة النتج من `f.read()` هو مقطع نصي.

```py
print(type(f.read()))

# Output
<class 'str'>
```

يدل `class str` على أنه مقطع نصي.

في هذه الحالة, يطبع المِلَفّ بالكامل لأن لم يُحدد الحد الأقصى من وحدات بايت (bytes), ولكن تستطع تحديد ذلك أيضاً.

مثل:

```py
f = open("data/names.txt")
print(f.read(3))
```

ينتج القيمة المحددة من عدد وحدات بايت:

```md
Nor
```

❗️**مهم:** تحتاج إلى غلق المِلَفّ بعد أكتمال الغرض؛ حتي تحرر الموارد المرفقة بالمِلَفّ. لفعل ذلك, تحتاج إلى أستخدام طريقة `close()`, مثل:

![image-22](https://user-images.githubusercontent.com/88248797/187189876-74c50ada-8ccb-4fa2-8de4-620fbba04363.png)

### **طريقة `Readline()` مقابل `ReadLines()`**

يمكن قراءة سطراً في المِلَفّ باستخدام هاتين الطريقتين. يختلفوا قليلاً, لذلك ستري كيفية أستخدامهم بالتفاصيل.

تقرأ `readline()` **سطراً واحداً** من المِلَفّ حتي تصل إلى نهاية السطر. أن في واقع الأمر, تبحث الطريقة عن حرف الذي يدل على سطر جديد (`/n`) الذي يوجد في نهاية مقطع نصي.


💡 **تلميح:** يمكن أختيار إضافة حجم, ينتج ذلك مقطع نصي من أقصي عدد من الحروف التي تريد أضافتها.

![image-19](https://user-images.githubusercontent.com/88248797/187197862-0f0bce7c-156b-46fa-8cc5-e8e8fab4779d.png)

مثل:

```py
f = open("data/names.txt")
print(f.readline())
f.close()
```

وينتج أول سطر:

```md
Nora
```

بخلاف ذلك, فإن `readlines()` ينتج **قائمة سطور** من المِلَفّ كعناصر منفصلة (مقاطع نصية). تكتب بشكل: 

![image-21](https://user-images.githubusercontent.com/88248797/187198754-28c4566f-d763-4b58-8e82-0bec9162ac02.png)

مثل

```py
f = open("data/names.txt")
print(f.readlines())
f.close()
```

وينتج:

```md
['Nora\n', 'Gino\n', 'Timmy\n', 'William']
```

لاحظ وجود حرف الذي يدل على سطر `/n` في نهاية كل مقطع نصي, باستثناء الأخير.

 💡 **تمليح:** يمكنك الحصول على نفس القائمة بواسطة `list(f)`.

يمكنك التعامل مع القائمة في برنامجك أرفاقها إلى متغير أو بواسطة استخدام وظيفة الحلقة:

```py
f = open("data/names.txt")

for line in f.readlines():
    # Do something with each line
    
f.close()
```

يمكنك تكرار الوظيفة على متغير `f` قاصداً (كائن المِلَفّ) في الحلقة:

```py
f = open("data/names.txt", "r")

for line in f:
	# Do something with each line

f.close()
```

وبذلك تعلمت الطرق الأساسية لقراءة كائنات المِلَفّ. ولكن يمكنك إنشاء مِلَفّات أيضاً.

## 🔹 كيفية إنشاء المِلَفّ 

عند الحاجة لإنشاء مِلَفّ "بشكل حيوي" باستخدام Python, يمكن فعل ذلك باستخدام طريقة `"x"`.

تكتب بهذا الشكل:

![image-58](https://user-images.githubusercontent.com/88248797/187476765-25d77ed6-3649-4f41-a521-2932d5e5596c.png)

هذا هو مثال عن شكل المستند الذي تعاملت معه:

![dictonary](https://user-images.githubusercontent.com/88248797/187477304-730a8651-e6d6-471b-8a00-40e32d65c382.png)

أذا تم تفعيل هذا السطر من التعليمات البرمجية:

```py
f = open("new_file.txt", "x")
```

يتم أنشاء مِلَفّ جديد باسم `new_file`:

![creating new_file](https://user-images.githubusercontent.com/88248797/187477796-d7832895-4537-43d6-b855-f933b2e2cc25.png)

يمكنك بهذه الطريقة إنشاء مِلَفّ وثم استخدام الطرق لكتابته بشكل حيوي, وسوف تتعلم ذلك.

💡 **تلميح:** سوف ينشئ المِلَفّ فارغاً حتي تكوم بتعديله.

عند محاولة تفعيل هذا السطر من التعليمات البرمجية مرة أخري ومع وجود مِلَفّ بنفس الاسم, سوف ترى هذا خطأ:

```py
Traceback (most recent call last):
  File "<path>", line 8, in <module>
    f = open("new_file.txt", "x")
FileExistsError: [Errno 17] File exists: 'new_file.txt'
```

وفقاً إلى [توثيق Python](https://docs.python.org/3/library/exceptions.html#FileExistsError), هذا يكون ألاستثناء (خظأ وقع في الوقت التفعيل):

> Raised when trying to create a file or directory which already exists.

هذا يخبرك أنك لا يمكنك إنشاء مِلَفّ أو مستند موجود فعلاً. وبهذا أنت تعرف كيفية أنشاء مِلَفّ و لماذا يفشل عندما تفعيل التعليمات البرمجية.

## 🔸 **كيفية تعديل مِلَفّ**

لتعديل (الكتابة في) المِلَفّ, تحتاج أستخدام طريقة `write()`. تملك طريقتين لفعل ذلك (ألحق `"a"` أو كتابة `"w"`) أستناداً على الطريقة التي تختارها لفتح المِلَفّ.

### **ألحق**

يعني "الألحاق" إضافة شيئاً ما ألى نهاية شيئاً أخر. تسمح لك طريقة `"a"`  بفتح مِلَفّ ولحق بعض المحتويات إليه.

عندما نملك مِلَفّ يشبه هذا:

![مِلَفّ يحتوي على محتوي](https://user-images.githubusercontent.com/88248797/187493530-d42bc265-0aca-46be-8e71-208f7a35d644.png)

وعند الرغبة في إضافة سطر جديد إليه, يمكن فتحه باستخدام طريقة `"a"`, ثم تفعيل طريقة `write()`, وذلك يُمرر المحتوي المرغوب إلحاقه كحجة.

هذا الإعراب المبدئي لاستخدام طريقة `write()`:

![image-52](https://user-images.githubusercontent.com/88248797/187494398-252149d0-86bd-480b-b4e6-b5e933b00a42.png)

وتكتب هكذا:

```py
f = open("data/names.txt", "a")
f.write("\nNew Line")
f.close()
```

💡 **تلميح:** لاحظ إضافة `/n` قبل السطر في طريقة `f.write("")` لإشارة بالرغبة في ظهور سطر جديد في سطر منفصل, وليس كاستمرار للسطر الموجود.

يكون هذا المِلَفّ بعد تفعيل العليمات:

![image-45](https://user-images.githubusercontent.com/88248797/187496180-e3b744f0-10e4-4647-a496-76013ce9da92.png)

💡 **التلميح:** يمكن عدم عرض السطر الجديد في المِلَفّ حتي تفعيل `f.close()`.

### **كتابة** 

أحياناً, ربما تحتاج ألى حذف محتوي المِلَفّ وتبديل بمحتوي جديد تماماً. يمكنك فعل ذلك بواسطة طريقة `write()` عند رغبتك فتح المِلَفّ بواسطة طريفة `m`.

هذا كيف سيبدو المِلَفّ:

![image-43](https://user-images.githubusercontent.com/88248797/187976276-517be9bc-bc0f-40db-a3ba-87fa594b6685.png)

عند تفعيل التعليمات:

```py
f = open("data/names.txt", "w")
f.write("New Content")
f.close()
```

سوف تنتج:

![image-46](https://user-images.githubusercontent.com/88248797/187976438-cc0067c9-f6d9-4c73-a67a-44d30d6880d0.png)

كما تري, سوف تم فتح مِلَفّ مع طريقة `"w"`, ثم كتابة محتوي جديد يبدل المحتوي السابق.

💡 **تلميح:** تنتج طريقة `write()` عدد الحروف المرغوب كتابتها.

عند الرغبة بفتح عدد سطور في وقت واحد, يمكنك أستخدام طريقة `writelines()`, الذي تستخدم قائمة من المقاطع كحجة. يمثل كل مقطع سطر يتم أضافته إلى المِلَفّ.

يكون المِلَفّ الأولى يشبه:

![image-43](https://user-images.githubusercontent.com/88248797/187977839-cd058da8-0cb3-4274-9d90-d262bca9a8a0.png)

عند تفعيل هذه التعليمات:

```py
f = open("data/names.txt", "a")
f.writelines(["\nline1", "\nline2", "\nline3"])
f.close()
```

إضافة عدد الأسطر إلى نهاية المِلَفّ:

![image-47](https://user-images.githubusercontent.com/88248797/187978113-5f23b6d7-2f8e-4f6b-9b7f-07af70bd8b1f.png)


### **فتح مِلَفّ لاستخدام العديد العمليات**

ألان تعرف كيفية أنشاء, وقراءة, وكتابة المِلَفّ. ولكن ماذا يحدث عندما ترغب بفعل ذلك الطرق أكثر من مرة في نفس البرنامَج؟ سوف تري ماذا يحدث عندما تحاول فعل ذلك باستخدام الطرق الذي تعلمتها:

عندما تفتح مِلَفّ بواسطة طريقة `"r"` (قراءة), وثم حاول كتابة المحتوي في المِلَفّ:

```py
f = open("data/names.txt")
f.write("New Content") # Trying to write
f.close()
```

سوف تحصل علي هذا الخطأ:

```py
Traceback (most recent call last):
  File "<path>", line 9, in <module>
    f.write("New Content")
io.UnsupportedOperation: not writable
```

علي سبيل المثال, عند فتح المِلَفّ في طريقة `"w"` (كتابة), ثم محاولة قراءته:

```py
f = open("data/names.txt", "w")
print(f.readlines()) # Trying to read
f.write("New Content")
f.close()
```

سوف تري هذا الخطأ:

```py
Traceback (most recent call last):
  File "<path>", line 14, in <module>
    print(f.readlines())
io.UnsupportedOperation: not readable
```

سوف يحدث المثل في طريقة `"a"` (ألحاق).

عند الرغبة في قراءة المِلَفّ وأجراء عملية أخرى في نفس البرنامَج, ستحتاج إلى إضافة `"+"` الرمز إلى الطريقة, مثل:

```py
f = open("data/names.txt", "w+") # Read + Write
```

```py
f = open("data/names.txt", "a+") # Read + Append
```

```py
f = open("data/names.txt", "r+") # Read + Write
```

يوجد أحتمال هذا ما ترغب باستخدامه في برنامجك, لكن تحقيق من إضافة الطرق فقط لتجنب الأخطاء المحتملة.

## 🔹 **كيفية حذف المِلَفّات**

أحياناً لا تحتج المِلَفّات بعد أستخدامها, لحذفهم باستخدام Python, سوف تحتاج إلى أستراد وحدة نمطية تسمى `os` التي تحتوي وظائف التي تتعامل مع نظام تشغيلك.

💡 **تلميح:** تكون الوحدة النمطية مِلَفّ Python مع متغيرات, ووظائف, وفئات ذات صله إليه.

خصوصاً, سوف تحتاج وظيفة `function()`. سوف تأخذ الوظيفة المسار إلى المِلَفّ كحجة وتحذف المِلَفّ تلقائياً.

![image-56](https://user-images.githubusercontent.com/88248797/187986066-4f729db7-e1d5-4f5b-b01c-25812e65da2c.png)

في المثال. يوجد مِلَفّ يسمي `sample_file.txt` يمكن حذفه.

![image-34](https://user-images.githubusercontent.com/88248797/187986281-396a9f56-32d7-4eeb-97d1-c011a1a54a9d.png)

لفعل ذلك, تكتب التعليمات البرمجية:

```py
import os
os.remove("sample_file.txt")
```

- يتكون السطر الأول من `import os` وتسمى "تعبير أستراد". يكتب التعبير بأعلى مِلَفّك ويسمح لك باستخدام الوظائف المحددة في الوحدة النمطية `os`.

- بينما يتكون السطر الثاني من `os.remove("sample_file.txt")` الذي يحذف المِلَفّ المرغوب به.

💡 **تلميح:** يمكنك أستخدام مسار مطلق أو نسبي.

 يحتوي Python علي أداة التي تدير المحتوي وتلك الأداة تسهل التعامل مع المِلَفّ.

## 🔸 أدوات أدارة المحتوي

تكون أداة أدارة المحتوي منشئات من Python التي تيسر حياتك. لا تحتج إلى إن تتذكر غلق مِلَفّك في نهاية برنامجك وتملك منفذ ألى المِلَفّ في جزء خاص (من أختيارك) في برنامجك.

### تركيب الجملة

يحتوي أداه أدارة المحتوي على ثالث أركان (كلمة أساسية, كائن المِلَفّ, متغير يشير إلى كائن المِلَفّ):

![image-33](https://user-images.githubusercontent.com/88248797/188272924-1f163a3e-f24f-48d1-ae06-5144b8bd9d2e.png)

💡 **تلميح:** يجب إضافة مسافة إلى هيكل في أداه أدارة المحتوي, مثل إضافة مسافة عند أستخدام الحلَقات, الوظائف, والفئات. عند عدم وجود مسافة, سوف يعدّ البرنامَج الهيكل جزء من الأداة.

عند أكتمال هيكل, سوف يتم غلق المِلَفّ لقائيا, ويكون الجملة مثل:

```py
with open("<path>", "<mode>") as <var>:
    # Working with the file...

# The file is closed here!
```

مثال:

```py
with open("data/names.txt", "r+") as f:
    print(f.readlines())
```

يفتح أداه أدارة المحتوي مِلَفّ `names.txt`, ويسمح بعمليات القراءة والكتابة, ويعين كائن المِلَفّ إلى المتغير `f`. يستخدم المتغير في الهيكل للإشارة إلى كائن المِلَفّ.

### **محاولة قرائة المِلَفّ مرة أخري**

بعد تفعيل المهام المرغوبة فيها من الهيكل, يُغلق المِلَفّ تلقائياً, ولكن لا يمكن قراءته دون فتحوه مرة أخرى. ولكن ماذا يحدث عند محاولة قراءة المِلَفّ مرة أخري:

```py
with open("data/names.txt", "r+") as f:
    print(f.readlines())

print(f.readlines()) # Trying to read the file again, outside of the context manager
```

تنتج هذه الرسالة:

```py
Traceback (most recent call last):
  File "<path>", line 21, in <module>
    print(f.readlines())
ValueError: I/O operation on closed file.
```

يظهر هذا الخطأ عند محاولة قراءة مِلَفّ مغلق. تقوم أداه أدارة المحتوي بالمهام الشاقة لأجلك, وتكون سهل قراءتها وموجزة.

## 🔹 **كيفية التعامل مع الإخطاء الناتجة من ألاستثناءات عند التعامل مع المِلَفّ**

عند تعاملك مع المِلَفّات, يمكن أن يحدث أخطاء مثلما رأيت في هذا الموضوع. يكون خطاء أخر ألا تملك صلاحيات الضرورية لتعديل والوصول إلى المِلَفّ, أو عدم وجود مِلَفّ.

كمبرمج, تحتاج توقع هذه الظروف ومعالجتها, لتجنب تهشم مفاجئ في البرنامَج الذي يأثر على تجرِبة المستخدم.

يكونوا الأخطاء الأكثر شيوعاً الذي يمكن إن تواجها عند التعامل مع مِلَفّات, هن:

### **FileNotFoundError**

وفقاً [لتوثيق Python](https://docs.python.org/3/library/exceptions.html#FileNotFoundError), يكون الاستثناء:

> Raised when a file or directory is requested but doesn’t exist.

وهذا يدل على عدم وجود المِلَفّ أو المستند المطلوب. فهذا الاستثناء يحدث عند محاولة فتح مِلَفّ في المجلد:

```py
f = open("names.txt")
```

ستري هذا الخطاء:

```py
Traceback (most recent call last):
  File "<path>", line 8, in <module>
    f = open("names.txt")
FileNotFoundError: [Errno 2] No such file or directory: 'names.txt'
```

يكون هذا ألاستثناء من هذه السطور:

- يخبرك أول سطر `File "<path>", line 8, in <module>` لقد وقع الخطأ عند تفعيل التعليمات البرمجية بالمِلَفّ الواقع في `<path>`, وبالأخص عند محاول `line 8` تفعيل `<module>`.
- يحدث الخطأ في السطر الثاني `f = open("names.txt")`.
- يوضح السطر الثالث `FileNotFoundError: [Errno 2] No such file or directory: 'names.txt'` إن الاستثناء `FileNotFoundError` يحدث إذا عدم وجود مِلَفّ أو مجلد باسم `names.txt`.

💡 **لاحظ:** يكون Python شفاف جداً في رسائل الأخطاء, وتساعدك هذه مِيزة في مسارك لتصحيح التعليمات البرمجية.

### **PermissionError**

يكون الأستثناء شائع عند التعامل مع المِلَفّات. وفقاً إلى [توثيق Python](https://docs.python.org/3/library/exceptions.html#PermissionError):

> Raised when trying to run an operation without the adequate access rights - for example filesystem permissions.

يخبرك حدوث ألاستثناء إنك لا تملك التصريح لتعديل أو قراءة المِلَفّ. عند محاولة قراءة مِلَفّ ولا يوجد إذن لك باستخدامه, سوف ترى هذا الخطاء: 

```py
Traceback (most recent call last):
  File "<path>", line 8, in <module>
    f = open("<file_path>")
PermissionError: [Errno 13] Permission denied: 'data'
```

### **IsADirectoryError**

وفقاً إلى [توثيق Python], يكون هذا ألاستثناء:

> Raised when a file operation is requested on a directory.

يقع هذا ألاستثناء عند محاولة فتح أو تعامل في المجلد بدلاً من مِلَفّ, لذلك توخي الحظر عند تمرر الحَجَّة.

### **كيفية التعامل مع الاستثناءات**

عندما تواجه الاستثناءات في برنامجك يتوقف برنامجك عن العمل تماماً, ولكن يوجد في Python وسيلة تجعل من الممكن أستمرار البرنامَج على العمل حتي عند وقوع الاستثناء, تسمي تعبير **`try/except`**.

يمكن استخدام التعبير في برنامجك في حالة وقوع حدث غير متوقع. يكتب التعبير المبدئ بهذا الشكل: 

```py
try:
	# Try to run this code
except <type_of_exception>:
	# If an exception of this type is raised, stop the process and jump to this block
```

أستثناء `FileNotFoundError`:

```py
try:
    f = open("names.txt")
except FileNotFoundError:
    print("The file doesn't exist")
```

يخبر هذه التعليمات التالي:

- حاول فتح مِلَفّ يسمى `name.txt`.
- عند وقوع `FileNotFoundError`, لا يتوقف البرنامَج وأطبع بيان واضح إلى المستخدم.

💡 **تلميح:** يمكنك أختيار كيفية الاندماج في الموقف خلال كتابة التعليمات المناسبة في مجموعة `except`. ربما ترغب في إنشاء مِلَفّ جديد أذا لم يكون المِلَفّ المرغوب فيه موجود فعلًا.

يمكن أغلاق المِلَفّ تلقائياً بعد المهمة (يغظ النظر عن وقع ألاستثناء أو لم يقع في مجموعة `try`) بواسطة إضافة مجموعة `finally`.

```py
try:
	# Try to run this code
except <exception>:
	# If this exception is raised, stop the process immediately and jump to this block
finally: 
	# Do this after running the code, even if an exception was raised
```

مثال:

```py
try:
    f = open("names.txt")
except FileNotFoundError:
    print("The file doesn't exist")
finally:
    f.close()
```

يوجد العديد من الطرق لتصميم تعبيرات try/except/finally ويمكنك إضافة مجموعة `else` لتفعيل مجموعة من التعليمات عندما لا يوجد أستثناء وقع في مجموعة `try`.

💡 **تلميح:** يمكنك التعلم المزيد عن تعامل مع الاستثناءات في Python في هذا المقال بالانجليزية: ["How to Handle Exceptions in Python: A Detailed Visual Introduction".](https://www.freecodecamp.org/news/exception-handling-python/).

## 🔸 ملخص

- يمكنك قراءة, وكتابة, وحذف المِلَفّات باستخدام Python.
- يملك كائنات المِلَفّ مجموعة من طرق الذي تستطيع استخدامها في برنامجك.
- تساعدك أداة أدارة المحتوى على التعامل مع المِلَفّات وإدارتهم, عن طريق غلقهم تلقائياً عند أكتمال المطلوب.
- تعرفت إلى استثناءات شائعة الواقعة في المِلَفّات مثل: `FileNotFoundError`, و `FileNotFoundError`, و `IsADirectoryError`. يمكنك استخدام try/except/else/finally للتعامل مع الاستثناءات.

كتب المقال الأصلي بواسطة [Estefania](https://www.freecodecamp.org/news/author/estefaniacn/), يمكن متابعتهم حسابهم في [Twitter](https://twitter.com/EstefaniaCassN).
