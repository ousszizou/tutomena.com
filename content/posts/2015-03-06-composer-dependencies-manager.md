---
title: 'ماهو Composer ؟'
date: '2015-03-06'
slug: 'web-development/tools/composer-dependencies-manager'
template: 'post'
categories:
  - أدوات
tags:
  - autoload
  - composer
  - dependency
  - faker
  - php
thumbnail: '../thumbnails/php.png'
---

Composer هو أداة لإدارة الرزم أو dependencies الخاص [بلغة PHP](/web-development/php/why-php-is-so-popular/) ويعتمد على الملف `composer.json` الذي يحتوي على معلومات عدة حول المشروع ومنها الرزم أوالمكتبات المستعملة في هذا المشروع ويقوم بتوليد أو إنشاء ما يصطلح عليه بال autoloader الذي يقوم بالإستدعاء التلقائي للكلاسات داخل هذه المكتبات بعد تحميلها حتى يتم استعمالها في المشروع بسهولة وبساطة.

## تنصيب Composer

تنصيب Composer ليس بالأمر الصعب، سواء كنت في نظام ويندوز أو أحد أنظمة Unix ما عليك إلا تنفيذ هذا الأمر في Terminal حتى يتم تثبيت Composer على جهازك.

> إذا واجهتك صعوبات فالمرجو العودة إلى [هذه الصفحة](https://getcomposer.org/download/ 'تنصيب Composer') واتبع التعليمات الواردة فيها.

## كيف يعمل

كما أشرنا إليه سالفا، أول ما عليك فعله بعد تنصيب Composer هو إنشاء الملف composer.json وهناك ستضيف الرزم أو المكتبات التي تريدها في مشروعك، وفي مثالنا هذا سنختار النسخة 1.4.0 لمكتبة [Faker](/web-development/php/seeding-database-using-faker/).

```json
{
  "require": {
    "fzaninotto/Faker": "1.4.0"
  }
}
```

بعدما الإنتهاء من `composer.json` نعطي Composer الأمر بتحميل الرزمة أو المكتبة وذلك بتنفيذ الأمر `php composer.phar install` في Terminal أو Command Line.

> يقوم Composer بتحميل الرزم من [هذا الموقع](https://packagist.org/ 'Packagist') ولو افترضنا أن مكتبة Faker بحاجة لمكتبة أخرى لكي تعمل فسيقوم Composer بتحميلها أيضا تلقائيا.

بعد تنفيذ الأمر السابق سيقوم Composer إضافة ملف Folder اسمه vendor إلى مشروعك ويضم كل عناصر الرزم التي قام بتحميلها.

## استدعاء المكتبات أو الرزم

في داخل الملف vendor الذي قام Composer بإضافته ستجد ملفا اسمه autoload.php وهو الوحيد الذي سنقوم باستدعائه في مشروعنا بحيث سيتكفل هو باستدعاء كل كلاس في هذه الرزمة أوتوماتيكيا كلما أنشأنا كائنا من هذا الكلاس في تطبيقنا وهذا ما يعرف بال autoloading في PHP.

كل ما علينا فعله هو تحديد النطاق أو namespace الخاص بالكلاس قبل استدعائها كما ستلاحظون في المثال التالي :

```php
require 'vendor/autoload.php';
$faker = Faker\Factory::create();
```

كما لاحظتم استعملنا اسم النطاق Faker متبوعا بالرمز back slash قبل اسم الكلاس Factory.

هذا هو **Composer** ببساطة، لو أردنا مثلا إضافة مكتبة أخرى للمشروع فكل ما علينا فعله هو إضافة اسمها والنسخة التي نريدها في ملف `composer.json` تماما كما فعلنا مع مكتبة Faker وبعد ذلك نقوم بتنفذ الأمر `php composer.phar update` في Terminal حتى يقوم Composer بتحميلها ويقوم كذلك بتحديث ملف autoload.php. الآن لو كنت تعمل مع صديق لك على نفس المشروع فكل ما عليك فعله هو أن ترسل له ملف `composer.json` وسيقوم بتحميل كل الرزم ببساطة باتباع نفس الخطوات السابقة.

نرجو أن تستفيدوا من هذا الدرس وتبدؤو بالإستفادة من قوة Composer في مشاريعكم خاصة أن العديد من المشاريع الكبرى ل PHP مثل Laravel و Symfony بدأت تعتمد عليه، وإذا كانت لديكم أية أسئلة أو ملاحظات فلا تترددوا بطرحها في منطقة التعليقات أسفله. السلام عليكم.
