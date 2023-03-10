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

* Started by creating the enum in the model directory.
* Instead of `TaskInfoStatus`, I called it `TaskStatus`, because it was now gonna be used on both _Task_ and _TaskInfo_.

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

* I exchanged the String on both and made them `TaskStatus`.

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

* I learned how to build my project by following the [CONTRIBUTING][contributing] guidelines. 
* And finally, succesfully edited the unit tests that used _Task_ and _TaskInfo_ `TaskStatus`.

After making all the changes, I had a question, but I needed to get some feedback to see if what I implemented was good, so I opened a draft pull request with the following question:

<p align="center">
    <img src="https://github.com/TheClerici/my-blog/blob/main/images/cleriq1.png?raw=true">
</p>
<div align="center">
    <h5><strong>Fig 2. GitHub 1st question</strong></h5>
</div>

Where I got the following response:

<p align="center">
    <img src="https://github.com/TheClerici/my-blog/blob/main/images/alallematwo.png?raw=true">
</p>
<div align="center">
    <h5><strong>Fig 3. GitHub 2nd feedback</strong></h5>
</div>

With this in consideration, I started to work on what ale told me, but I was not clear about on how to modify wait for task, so I asked for a little hint. 

<p align="center">
    <img src="https://github.com/TheClerici/my-blog/blob/main/images/cleriq2.png?raw=true">
</p>
<div align="center">
    <h5><strong>Fig 4. GitHub 2nd question</strong></h5>
</div>

Where I got the following response:

<p align="center">
    <img src="https://github.com/TheClerici/my-blog/blob/main/images/alallema3.png?raw=true">
</p>
<div align="center">
    <h5><strong>Fig 5. GitHub 3rd feedback</strong></h5>
</div>

With this information, I can continue and finish what I started.

First, I modified the `testCreateDump()` on `ClientTest.java`, which was a matter or switching an assertion so the integration tests can build with what I implemented. This was achieved by changing:

```java
assertEquals(task.getStatus(), "enqueued");
```

To: 

```java
assertEquals(task.getStatus(), TaskStatus.ENQUEUED);
```

I also modified all of the tests that used the ENUM instead of just some of them, by doing it, all unit test where running succesfully.

To end with, I finished with what was breaking the code, which I asked for a hint, TaskStatus was a String that was being created as `""`, so I switched that to TaskStatus and initiated it as a null. Then, I deleted two Strings that were impersonating an ENUM at the beginning of the class, as they were not gonna be used anymore because we now have TaskStatus. And finally, I followed the hint that ala gave me and implemented the new while that stops the code to break. 

```java
public class TasksHandler {
    private final HttpClient httpClient;
    /* public static final String SUCCEEDED = "succeeded";  #Removed
    public static final String FAILED = "failed";           #Removed */

    void waitForTask(int taskUid, int timeoutInMs, int intervalInMs) throws MeilisearchException {
        Task task;
        //String status = "";       #Removed
        TaskStatus status = null; //#Added
        long startTime = new Date().getTime();
        long elapsedTime = 0;
        
        //New while
        while (status == null
                || (!status.equals(TaskStatus.SUCCEEDED) && !status.equals(TaskStatus.FAILED))) {
                //...
                }
        }
    }
```

Then, I started meilisearch on docker, ran unit, integration and linter tests to verify everything was working, then, following the contribution guide I commented that it was ready and ala told me it looked good!! Here is where ala realized that it was an enhancement and added the label:

<p align="center">
    <img src="https://github.com/TheClerici/my-blog/blob/main/images/alellema4.png?raw=true">
</p>
<div align="center">
    <h5><strong>Fig 6. Enhancement label</strong></h5>
</div>

------------------------------------------------------------------------------------------
<blockquote> <p> How to contribute: </p> </blockquote> 

1. Choose a Contribution
    * The first step to contributing to MeiliSearch is to choose a contribution. This can be a new feature, a bug fix, documentation, or testing. MeiliSearch maintains a list of issues on GitHub that need attention, and this can be a good place to start.
2. Fork the Repository
    * After identifying the contribution, fork the MeiliSearch repository on GitHub. This creates a copy of the repository in your account, which you can use to make changes.
3. Set Up a Local Environment
    * Clone the forked repository to your local machine and set up a development environment. The MeiliSearch repository contains a Dockerfile and a docker-compose file, which can be used to set up a local environment quickly. Follow the instructions in the repository to set up the environment.
4. Create a New Branch
    * Create a new branch in the forked repository for the contribution. This helps to keep changes separate from the main codebase and makes it easier to manage changes. Name the branch appropriately, such as "new-feature" or "bug-fix".
5. Make Changes and Test
    * Make the necessary changes to the codebase and test them locally. MeiliSearch has a suite of tests that can be run locally to ensure that the changes do not break the codebase.
6. Commit Changes
    * After testing the changes, commit them to the branch with an appropriate commit message. The commit message should be descriptive and should explain the changes made.
7.  Push Changes and Create a Pull Request
    * Push the changes to the forked repository and create a pull request. The pull request should include a description of the changes made, any relevant documentation, and any other details that are necessary.
8. Address Feedback
    * The MeiliSearch team will review the pull request and provide feedback. Address the feedback and make any necessary changes.
9. Merge the Pull Request
    * Once the pull request has been approved, it can be merged into the main codebase. Congratulations, you have successfully contributed to MeiliSearch!

With the solution added, I just followed the guide instructions explained above to fully contribute to the project, it is now merged and with that, I succesfully contributed to my third open-source project!! See you next time!

[meili]: https://github.com/meilisearch
[cj-dor]: https://github.com/meilisearch/meilisearch-java/issues/556
[contributing]: https://github.com/meilisearch/meilisearch-java/blob/main/CONTRIBUTING.md