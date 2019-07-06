---
layout: post
date: 2019-06-22
title: أنواع أنظمة الملفات وكيفية الاختيار بينهم
description: شرح واضح ﻷشهر أنواع أنظمة الملفات والمقارنة بينهم وكيفية الاختيار الصحيح بحسب القرص واستخدامه FAT23,exFAT NTFS, ext, ext4, HFS
type: tutorial
comments: true
---

أهلًا بكم في درس جديد حول أنظمة الملفات File Systems والتي هي الأساس لتنظيم الملفات في وحدات التخزين (الأقراص الصلبة).

يوجد اليوم العديد من أنظمة الملفات المستخدمة ويعود لك قرار اختيار أحدها عند تهيئته القرص الصلب وذلك وفقًا لـ :

* نظام التشغيل 
* نوع القرص الذي تقوم بتهيئته

ستجد في هذا المقال تغطية لـ 12 نوع شائع لنظام الملفات

دعونا في البداية نفهم سريعًا وظيفة أنظمة الملفات.

* Toc
{:toc}

# وظيفة أنظمة الملفات

تقوم بتقسيم مساحة القرص إلى حجرات (أقسام صغيرة) افتراضية وتعطي لكل ملف رقم تسلسلي يعبر عن مكان تواجده في القرص الصلب.

الصورة التالية توضح العملية حيث تعبر المربعات عن الحجرات وتعبر المساحات الحمراء عن حجم الملفات في كل حجرة

![File-Systems](/assets/file-systems.jpg)

(للمزيد حول فهم الموضوع نظريًا اقرأ عنه في [ويكيبيديا](https://ar.wikipedia.org/wiki/نظام_الملفات))


# FAT12, FAT16 & FAT32

أقدم أنواع الملفات في هذه القائمة وهو FAT12 المُصدر عام 1980 وبعدها FAT16 عام 1984 من قبل IBM وميكروسوفت ثم FAT32 من قبل ميكروسوفت عام 1996.
إن FAT اختصار لـ (File allocation table) وتعني جدول توزيع الملفات، الأنواع الرئيسية لها هي المذكورة هنا (FAT12-16-32) بحيث يشير ازدياد الرقم إلى زيادة في عدد الحجرات والحجم الأعظمي للملف الواحد ولحجم القرص بالكامل. وفيما يلي جدول يوضح ذلك:

|	|الحجم الأعظمي للملف الواحد | الحجم الأعظمي للقرص
|-----|------|---------
|FAT12|32MB|32MB
|FAT16|2GB/4GB[^1]|16GB
|FAT32|4GB|32GB (تهيئة ويندوز)
|||2TB (أنظمة أخرى)
|||16TB (نظريًا)

[^1]: الإصدارات المختلفة ل FAT16 محدودة لحجم ملفات أعظمي 2GB,4GB مع حجم قرص أعظمي 2GB أو 4 أو 8 أو 16 جيغابايت وذلك بحسب حجم القسم والحجرة.

**التوافق مع أنظمة التشغيل**: نظام الملفات FAT32 شائع جدًا بسبب توافقه مع أنظمة التشغيل المختلفة ويُستخدم كثيرًا لوحدات التخزين الخارجية من USB Flash وكروت الذاكرة للهواتف وما إلى ذلك..

# NTFS 
اختصار لـ New Technology File System وهو الأكثر شيوعًا ﻷنظمة ويندوز وتم إطلاقه عام 1993 لتجاوز حد حجم الملفات الموجود في FAT32 حيث أصبح الحد الأعظمي لحجم الملف الواحد 16 exabytes، والإكسابايت EB هي مليون تيرابايت، مما يعني أنه عمليا لايوجد حد لحجم الملف!

هذا النوع من أنظمة الملفات هو journaling File System أي يحتفظ بسجل للتغييرات وبالتالي يتم تجنب تلف البيانات ويتم الاستعادة في حال حدوث خلل في النظام أو في الطاقة الكهربائية.
وليس كما في FAT32، يدعم نظام الملفات هنا الصلاحية، مما يعني أنه يمكن مثلا الإشارة لملف ما على أنه للقراءة فقط، كما يدعم تشفير البيانات. مما يجعله مناسب أكثر لاستخدامه نظاما للملفات ﻷنظمة التشغيل، ولذا **يجب** تنصيب الويندوز على قرص ذو نوع نظام ملفات NTFS.

**التوافق مع أنظمة التشغيل**: غير متوافق مع الإصدارات القديمة لويندوز وكذلك غير متوافق مع الأنظمة الأخرى، مثلا تظهر أقراص NTFS على أنها للقراءة فقط في نظام macOS والأنظمة القديمة من لينكس. وقد لاتكون قابلة للقراءة نهائيًا لأجهزة مشغلات الفيديو مثلًا. بالتالي يجب عدم استخدامها للأقراص الخارجية

# exFAT

اختصار لـ Extended File Allocation Table تم إطلاقه من قِبَل ميكروسوفت عام 2006 كنظام مُحسَّن لأقراص USB كبيرة السعة وكروت الذاكرة.

نظام الملفات هذا أقل تطوّرًا من NTFS ولكن يحوي مزايا إضافية بالمقارنة مع FAT32. 
الحد الأعظمي لحجم الملف الواحد هنا هو 16EX أي عمليا لا يوجد حد. مما يجعله أفضل خيار لكروت الذاكرة التي تٌسجَّل عليها ملفات الفيديو. ولهذا السبب تم اختياره كنظام ملفات افتراضي لكروت ذاكرة SDXC

**التوافق مع أنظمة التشغيل**: يتوافق بشكل أفضل مع الأنظمة المختلفة بالمقارنة مع NTFS. بما في ذلك القراءة والكتابة على أنظمة ماك macOS والإصدارات الحديثة من أندرويد. وعلى اللينكس فستحتاج لتنزيل حزم إضافية للوصول لأقراص exFAT.

# ext2, ext3 & ext4

اختصار لـ extended File System وتم إطلاقه حصرًا ﻷنظمة لينكس عام 1992 حيث أُطلق نظام الملفات ext.
بعدها بعام أُطلق ext2 والذي كان لسنوات عديدة نظام الملفات الافتراضي للعديد من توزيعات لينكس.
عام 2001 تم إصدار ext3 والذي وفَّر journaling File System المذكور سابقّا لتجنب تلف البيانات.
وتم طرح أخيرًا ext4 عام 2008 الأحدث لتاريخ هذه الصفحة والافتراضي ﻷنظمة لينكس.
أقصى حد لحجم الملف هو 16TB ولحجم القرص 1EB 

**التوافق مع أنظمة التشغيل**: كونه مخصص لأنظمة لينكس فهو غير متوافق بشكل افتراضي مع أنظمة تشغيل ويندوز وماك، ولكن قد يصبح قابل للقراءة أو حتى الكتابة باستخدام برامج اضافية.

# HFS, HFS+ & APFS

حيث HFS اختصار لـ hierarchical File System أي نظام الملفات الهرمي وتم إطلاقه من أبّل عام 1995 لنظام ماك. ويدعم حجم أعظمي للملف 2GB وحجم أعظمي للقرص 2TB ويُعرف أيضًا بـ Mac OS standard.
وتم إطلاق HFS+ عام 1998 والذي يُعرف أيضًا بـ HFS Extended أو Mac OS Extended والذي يوفّر journaling لتجنب تلف البيانات ويدعم حجم أعظمي للملف والقرص 8EB عند استخدام نظام macOS 10 أو أحدث.
عام 2017 تم طرح نظام ملفات أبل Apple File System واختصارا APFS والمٌحسَّن ﻷقراص SSD.

**التوافق مع أنظمة التشغيل**: جميعهم لا يدعمون افتراضيًا الأنظمة الأخرى الغير تابعة لشركة أبّل

# ZFS

و zed file system الذي تم إطلاقه مبدأيًا عام 2006 من قِبَل Sun Microsystems ولكن منذ عام 2013 أصبح تطويره من قِبَل OpenZFS project.

يختلف نظام الملفات هذا عن باقي الأنظمة كونه يقوم بدمج مدير أقراص للتحكم بالأقراص المرتبطة بالحاسب. ومن خلال دمج إدارة القرص مع نظام الملفات، يوفّر ZFS حماية أكبر ضد فقد أو تلف البيانات.

**التوافق مع أنظمة التشغيل**: متوافق حاليًا مع لينكس و FreeBSD و TrueOS وقد يدعم ويندوز وماك لاحقًا.

# كيفية اختيار نظام الملفات

1. في حالة الأقراص التي سيتم تشغيل أنظمة التشغيل عليها فلا يوجد خيار هنا، حيث يجب عليك اختيار نوع نظام الملفات المٌختار أصلا من قبل نظام التشغيل الذي ستنصّبه. هذا يعني NTFS لويندوز و ext4 للينكس و HFS+ أو APFS للماك.

2. بالنسبة ﻷقراص USB وكروت الذاكرة فإن نظام الملفات FAT32 هو الخيار الأفضل للأقراص ذات السعة الأقل من 32 جيغابايت وذلك ﻷن له توافق مع مختلف الأنظمة (مع الانتباه إلى أن الحجم الأعظمي للملف كما هو مذكور 4 جيغابايت).

      أما لأقراص الـ USB وكروت الذاكرة ذات السعة أكبر من 32 جيغا أو إذا أردنا تخزين ملفات أكبر من 4 جيغا للملف الواحد فإن نظام الملفات exFAT هو الأفضل

3. للأقراص الخارجية عمومًا وأقراص SSD استخدم NTFS إذا كان الاستعمال يقتصر على أجهزة ويندوز، أو exFAT للاستعمال على كلا الويندوز والماك

آمل أن تكون قد حصلت على فائدة، إذا كان لديك أي سؤال فاطرحه في التعليقات، ﻷي تعديل أو اقتراح يمكن طرحه أيضًا في الأسفل أو تعديل الصفحة مباشرة من خلال الزر أعلى الصفحة.

# المراجع
* [Wikipedia](https://en.wikipedia.org/wiki/Comparison_of_file_systems)
* [ExplainigComputer channel on YouTube](https://www.youtube.com/watch?v=_h30HBYxtws)

