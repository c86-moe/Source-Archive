# Source Archive / Postscript Service
 This repo contains source code of GCG.moe's Source Archive. This code is independently developed and was used at https://src.gcg.moe/. A modified version was previously running at https://gcgsrc.csdcdo.org/ and https://script.gcg.moe/.

 Code contained in this repo has later been replaced since the refreshed version of postscript service was rolled out, which used more methods improve the codebase and to better efficiency.
 
 I am updating this repo to include all the later improvements before the refreshed / unified postscript service was released.

## Requirements
 - PHP 8.0+
 - MySQL
 - A compactable library of contents (under `lib` folder)
 - Microsoft Entra ID tenent with MS Graph capabilities.

## Setting up
There are several files needs to be changed before using this system.

1. Fill database and MS Graph information in `/inc/_config.inc` and then rename it to `/config.inc`.
2. Fill your turnstile secret and domain in `/inc/turnstile.php`.
3. Fill the database containing your data index to `/inc/connect.php`

During the later development stages, it was discovered that there are places where URL was somehow hardcoded - please change them before using this for places elsewhere

## Database
The database sample could be found in the SQL file. DO NOT UPLOAD THE SQL FILE TO YOUR WEBSITE.

Entry function represents the relation between files, titles, and categories, while a category represents relation with its type - a type could be configured as like but is represented by string instead of numbers.

For easy *direct* management and import, the way entries and categories connect it via two values, `type` and `typeid`, the pair of them should be unique. However, when using `category.php`, the passed parameter should be category's numerical id (PK).

## Content Format
 All contents stored here should end with `.txt.json`, this is to in comply with another tool developed to generate JSON files from acting script.

 Note: The refreshed postscript service uses an extended structure, and requires all files to end with `.json`.
 
 A most simple example of file is as follows:
 
 ```
{
  "1": [
    { "a": "speaker_1", "b": "line_1" },
    { "a": "speaker_2", "b": "line_2" },
    { "a": "(Option)", "b": "option_1", "c": "target_sectiom" }
  ],
  "target_section": [
    { "a": "speaker_1", "b": "line_1" },
    { "a": "speaker_2", "b": "line_2" }
  ]
}
```

Section 1 must exist, or the entry could not be properly loaded without section parameter. 
