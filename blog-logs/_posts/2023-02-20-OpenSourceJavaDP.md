---
layout: post
title:  "Translate the api-gateway readme to Spanish TechLog"
date:   2023-02-20 12:18:25 -0000
category: Log
---
## Translate the api-gateway readme to Spanish in Java Design Patterns.

------------------------------------------------------------------------------------------
<blockquote> <p> Overview: </p> </blockquote> 

Java design patterns showcases all of the different patterns that are used, which are formalized practices a programmer can use to solve problems when designing an app or system, they are often used to speed up the development process because they provide tested, proven development paradigms.

------------------------------------------------------------------------------------------
<blockquote> <p> Context: </p> </blockquote> 

[Translate to Spanish][cj-dor] issue:

This task tracks the translation of the patterns.

The main language is English, but we need to add translations for several other languages. For scenario 1) the user can browse to the correct language file and for scenario 2) we provide a language selector component in the top navigation (see the website).

The method for organizing the translations is to put them into directories named after the language code. The translated file still uses the original name (e.g. README.md)，just place it in the directory named after the language code.

* localization
 * fr
  * README.md
 * zh
  * README.md
  * abstract-document
   * README.md
  * abstract-factory
   * README.md
  * active-object
   * README.md

Acceptance criteria:

1. The patterns have been translated
2. The patterns can be browsed in Github and on the website https://java-design-patterns.com

------------------------------------------------------------------------------------------
<blockquote> <p> Solution: </p> </blockquote> 

The first challenge was to understand how the project I was going to contribute worked, after that, I needed to see the contributing guide so I can follow it, making sure to follow
GitHub's code of conduct for open-source projects, which stipulates that everyone must be gracious, respectful and professional.

I decided to open a new Issue so they can add it to the main issue I showed before, naming it Translate the api-gateway readme to Spanish, as I wanted to translate that part of the project.

In order to contribute, you need to check if your issue involves a new pattern, as it is not and we are working with a `Non-pattern Issue`, you need to follow these steps:

* Check that the issue is not yet in progress and has help wanted label
* Comment on the issue that you are working on it so that others don't work on the same thing. The maintainers will then assign the issue for you.
* Fork the repository.
* Implement the code changes in your fork. Remember to add sufficient comments documenting the implementation. Reference the issue id e.g. #52 in your commit messages.
* Create a pull request.

For this, I worked on the `API-gateway` README.md dile located on the spanish translations of the program /localization/es/api-gateway where I solve the issue, my approach was the following:

* Fork repo and clone it on my computer.
* Added folder and README.md file.
* Translate
* Add, commit and push to my fork.
* Pull request what I added.

With the solution added, I just followed the guide instructions explained above to fully contribute to the project, currently waiting for my pull request to be approved and merged and with that, I will succesfully contribute to my second open-source project!!

[cj-dor]: https://github.com/iluwatar/java-design-patterns/issues/2277