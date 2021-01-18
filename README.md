# Setup CodeSniffer (CS) in Drupal projects

Setup CS with composer:

```$ composer require drupal/coder:^8.3.1```
```$ composer require dealerdirect/phpcodesniffer-composer-installer```

Check codestandarts available in CS:

```$ vendor/bin/phpcs -i```

And you should see the following output (or something very similar):

```The installed coding standards are PEAR, Zend, PSR2, MySource, Squiz, PSR1, PSR12, Drupal, DrupalPractice and VariableAnalysis```

Put the file 'pre-commit' in '.git/hooks/pre-commit'.

Now CS run on each commit command and check files.

For example you can add tailing space in line

```define( 'WP_USE_THEMES', true ); ```

in your index.php file.
If you try to commit it you can see:

```
$ git add index.php
$ git commit -m "change index.php"
Checking PHP Lint...
No syntax errors detected in /.../index.php
Running Code Sniffer. Code standard WordPress.
E 1 / 1 (100%)



FILE: /.../index.php
----------------------------------------------------------------------
FOUND 1 ERROR AFFECTING 1 LINE
----------------------------------------------------------------------
 14 | ERROR | [x] Whitespace found at end of line
----------------------------------------------------------------------
PHPCBF CAN FIX THE 1 MARKED SNIFF VIOLATIONS AUTOMATICALLY
----------------------------------------------------------------------

Time: 219ms; Memory: 8MB

Fix the error before commit!
Run
  ./vendor/bin/phpcbf --standard=WordPress  /.../index.php
for automatic fix or fix it manually.
```

[Optional] Add in your '.gitignore' the line:

```vendor/```

[Optional] If you need to check not only .php files, please fix the 4th line in pre-commit file to:

STAGED_FILES_CMD=`git diff --cached --name-only --diff-filter=ACMR HEAD | grep \\\\.*`


## References

https://www.drupal.org/docs/contributed-modules/code-review-module/installing-coder-sniffer
https://www.drupal.org/node/1419988
