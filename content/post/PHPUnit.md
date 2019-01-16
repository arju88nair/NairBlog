---
title: "PHPUnit"
date: 2019-01-16T22:33:33+05:30
draft: false
tags: [
    "PHP",
    "Interview",
    Testing


]
---
[Source](https://phpunit.readthedocs.io/en/7.4/)

The tests for a `class` Class go into a class `ClassTest`.

`ClassTest` inherits (most of the time) from `PHPUnit\Framework\TestCase`.

The tests are public methods that are named `test*`.

Inside the test methods, `assertion` methods such as `assertSame`() (see Assertions) are used to assert that an actual value matches an expected value.

