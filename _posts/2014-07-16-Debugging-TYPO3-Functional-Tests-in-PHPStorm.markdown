---
layout: post
title:  "Debugging TYPO3 Functional tests with PHPStorm"
date:   2014-07-16 16:44:51
categories: debugging php programming xdebug phpstorm
---

Today I need to debug the TYPO3 functional tests with PHPStorm. While I am able to debug Unit Tests, the Functional Tests
seems to freeze right after starting from the command line.

The reason was quite simple: PHPUnit creates a new thread for every functional test. The new process stops right after its own creation and waiting for a debugger signal.

At the end I just needed to increase the number of allowed possible debugger connection in PHPStorm and I was able to debug functional tests as well.
