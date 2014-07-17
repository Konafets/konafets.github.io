---
layout: post
title: CodeCoverage in PHPStorm for TYPO3 Extensions
date:   2014-02-14 16:15
categories: TYPO3 PHPStorm PHP UnitTests
---

Finally I got CodeCoverage for my TYPO3 Extension right inside PHPStorm working. This article explain how it worked for me.

My setup:

* PHPUnit Installation via PEAR
* EXT:PHPUnit installed
* TYPO3 6.2 master
* the Core is located at `~/Developer/TYPO3/CMS/Core/master`
* the Extension is located at `~/Developer/TYPO3/CMS/Extensions/git/exampleExtension`
* the webroot pointing to `~/Sites/TYPO3/example.com/http`
* The core and the extension is symlinked into  webroot as in a usual TYPO3 installation

I configured the PHPStorm according the very good [article from Helmut Hummel](http://typo3.helmut-hummel.de/post/63972451370/executing-typo3-cms-unit-test-tests-in-phpstorm "Executing TYPO3 CMS Unit Test in PHPStorm")  with some small adjustments.
in `Run/Debug Configuration` set the `TestScope` to `Directory` and the directory should point to `~/Developer/TYPO3/CMS/Extensions/git/exampleExtension/Tests`

Hit the green Play-Button to ensure the setup works. If it does, hit the CodeCoverage-Button to execute the tests with CodeCoverage. This could take a moment and when its done PHPStorm gives you some feedback in the RunConsole:

    $ /opt/local/bin/php -dxdebug.coverage_enable=1 /private/var/folders/pc/pc6t79nd63vcqwx83w4zmcn00000gn/T/ide-phpunit.php --coverage-clover /Volumes/HDD/Users/$username/Library/Caches/WebIde70/coverage/http$exampleExtension.coverage --bootstrap /Volumes/HDD/Users/$username/Sites/TYPO3/example.com/http/typo3/sysext/core/Build/UnitTestsBootstrap.php --no-configuration /Volumes/HDD/Users/$username/Development/TYPO3/Extensions/git/exampleExtension/Tests

Replace `$username` with your user!


I highlighted the line of interest in this output. This is the file where PHPStorm writes the Coverage data.

Move or copy it into the webroot and rename it into a sane name with XML extension:

    $ mv ~/Library/Caches/WebIde70/coverage/http\$exampleExtension.coverage ~/Sites/TYPO3/example.com/http/exampleExtension.xml

If you grep through the file, you will see that the path to your extension is the real path on the server and NOT the path via the symlink.

    $ cat exampleExtension.xml | grep exampleExtension

    <file name="/Volumes/HDD/Users/$username/Sites/TYPO3/thesis.typo3_6-2.dev/http/typo3conf/ext/exampleExtension/Classes/Controller/Foo.php">

PHPStorm isn't able to connect these files with the CoverageData because this path is outside of the project. So we need to adjust this path by the webroot path.

    $ sed 's;/Volumes/HDD/Users/$username/Development/TYPO3/Extensions/git/;/Volumes/HDD/Users/$username/Sites/TYPO3/example.com/http/typo3conf/ext/;' exampleExtension.xml > exampleExtension-fixed.xml

Ensure that the pathes are correct now

    $ cat exampleExtension-fixed.xml | grep exampleExtension

In PHPStorm go to the `Help Menu` and select the first item `Find Action` and type `Show CodeCoverage Data` and hit the result. In the popup add a new Entry, select the `exampleExtension-fixed.xml` and after a click on `Show selected` you should see the Coverage summary on the right side of the IDE. Its also shown inside of the editor.