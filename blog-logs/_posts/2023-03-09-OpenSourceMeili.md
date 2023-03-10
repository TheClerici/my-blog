---
layout: post
title:  "Create an enum to handle the Task Status TechLog"
date:   2023-03-09 12:18:25 -0000
category: Log
---
## Create an enum to handle Status in Task and TaskInfo in MeiliSearch, modify tests and methods where it's used.

------------------------------------------------------------------------------------------
<blockquote> <p> Overview: </p> </blockquote> 

[MeiliSearch][meili] is a powerful and versatile open-source search engine designed to offer blazing-fast search capabilities for any kind of textual data. Unlike many other search engines that rely on a more complex and resource-intensive infrastructure, MeiliSearch is lightweight and easy to use, which makes it an excellent option for developers who need a reliable search engine that can be easily integrated into their applications.

At its core, MeiliSearch is built on top of several cutting-edge technologies such as Rust, Raft, and LMDB, which allow it to deliver lightning-fast search results even for large-scale data sets. Its powerful indexing engine and simple RESTful API make it easy to index, search, and retrieve data, while its flexible query syntax and support for a variety of languages and frameworks ensure that it can be seamlessly integrated into any application stack.

------------------------------------------------------------------------------------------
<blockquote> <p> Context: </p> </blockquote> 

[Create an enum to handle the Task Status][cj-dor] issue:

Currently, the Task status in TaskInfo is a String

```java
public class TaskInfo {
    protected String status = "";
    protected int taskUid = 0;
    protected String indexUid = "";
    protected String type = null;
    protected Date enqueuedAt = null;

    public TaskInfo() {}
}
```

But the status could only be one of this value: `enqueued`, `processing`, `succeeded`, `failed`, `canceled`.

It could be great to create an enum to handle this.

`NOTE:` As we progress with this pull request, methods and tests needed to be modified, alallema also asked to implement it not only on TaskInfo but also in Task and change the way it worked, adding the enhancement label after... so it is just not as simple as it looks! I will explain and show conversation screenshots in solution.

------------------------------------------------------------------------------------------
<blockquote> <p> Solution: </p> </blockquote> 

The first challenge was to understand how the project I was going to contribute worked, after that, I needed to see the contributing guide so I can follow it, making sure to follow
GitHub's code of conduct for open-source projects, which stipulates that everyone must be gracious, respectful and professional.

With this being adressed, I decided to start on the issue. 

I have only worked with fresh projects where I can set the enum I want from the beginning, this being said, this project already had a String that worked as an enum which only had five possible options. As I was not certain about that I decided to go simple with what I know, and added a new package called ENUMS, where I had my new enum with all possible words, changed it on TaskInfo and modified some but not all tests. When submitting it, alallema left a comment with further explanation on what was needed. 

<p align="center">
    <img src="https://github.com/TheClerici/my-blog/blob/main/images/alallemaone.png?raw=true">
</p>
<div align="center">
    <h5><strong>Fig 1. GitHub 1st feedback</strong></h5>
</div>

After getting my first feedback, I closed that pulled request and started again, as I felt like a needed a fresh start, this time, I was taking in consideration what I was told, and now needed to implement multiple things and have it in the order that they need.

1. Started by creating the enum in the model directory.
2. Instead of `TaskInfoStatus`, I called it `TaskStatus`, because it was now gonna be used on both _Task_ and _TaskInfo_.

```java
public enum TaskStatus {
    ENQUEUED("enqueued"),
    PROCESSING("processing"),
    SUCCEEDED("succeeded"),
    FAILED("failed"),
    CANCELED("canceled");

    public final String taskStatus;

    TaskStatus(String taskStatus) {
        this.taskStatus = taskStatus;
    }

    @Override
    public String toString() {
        return this.taskStatus;
    }
}
```

3. I exchanged the String on both and made them `TaskStatus`.

```java
public class Task {
    //protected String status = "";
    protected TaskStatus status = null;
    //Other params
}
public class TaskInfo {
    //protected String status = "";
    protected TaskStatus status = null;
    //Other params
}
```

4. I learned how to build my project by following the [CONTRIBUTING][contributing] guidelines. 
5. And finally, succesfully edited the unit tests that used _Task_ and _TaskInfo_ `TaskStatus`.

After making all the changes, I had a question, but I needed to get some feedback to see if what I implemented was good, so I opened a draft pull request with the following question:

<p align="center">
    <img src="https://github.com/TheClerici/my-blog/blob/main/images/cleriq1.png?raw=true">
</p>
<div align="center">
    <h5><strong>Fig 1. GitHub 1st question</strong></h5>
</div>

Where I got the following response:

<p align="center">
    <img src="https://github.com/TheClerici/my-blog/blob/main/images/alallematwo.png?raw=true">
</p>
<div align="center">
    <h5><strong>Fig 1. GitHub 1st feedback</strong></h5>
</div>

CONTINUE HER--------E

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

[meili]: https://github.com/meilisearch
[cj-dor]: https://github.com/meilisearch/meilisearch-java/issues/556
[contributing]: https://github.com/meilisearch/meilisearch-java/blob/main/CONTRIBUTING.md