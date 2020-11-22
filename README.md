# How to create a multi-project with Gradle
Recipe showing how to create a multi-project with gradle starting with cloning a brand new GitHub project.  We will
create two sub-projects: _service-api_ and _service-client_.  This is to simulate the development of a microservice 
along with a client.  The client will be a library where other microservice can import to encapsulate the mechanics 
of calling the public REST endpoints.  But because both, the _service-api_ and _service-client_ are closely 
related and owned by the same team, they will be both part of the same GitHub repository.

## 1. Create a new GitHub Repository.

Simply use the instructions from [GitHub Docs](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/create-a-repo)

Note that in this particular case, I do not create a gradle project aside of the repo and copy its content once I
cloned the repo.  Instead, we will clone this repo first and then, directly within the cloned repo directory, we
will call `gradle init`.

## 2. Clone the empty GitHub Repository

```shell script
itjraymond $ git clone git@github.com:itjraymond/gradle-multi-proj-setup.git
> Cloning into 'gradle-multi-proj-setup'...
> remote: Enumerating objects: 4, done.
> remote: Counting objects: 100% (4/4), done.
> remote: Compressing objects: 100% (4/4), done.
> Receiving objects: 100% (4/4), done.
> remote: Total 4 (delta 0), reused 0 (delta 0), pack-reused 0

itjraymond $ cd gradle-multi-proj-setup/
itjraymond $ ls -la
> total 16
> drwxr-xr-x   5 jraymond  staff  160 22 Nov 11:00 .
> drwxr-xr-x  20 jraymond  staff  640 22 Nov 11:00 ..
> drwxr-xr-x  12 jraymond  staff  384 22 Nov 11:00 .git
> -rw-r--r--   1 jraymond  staff  278 22 Nov 11:00 .gitignore
> -rw-r--r--   1 jraymond  staff  131 22 Nov 11:00 README.md

```

As we can see, we currently only have the README.md file (this file :-)

## 3. Create Gradle multi-project structure.

Once we cloned the empty GitHub project and changed directory to it, we can execute a `gradle init` command.

```shell script
itjraymond $ gradle init

Select type of project to generate:
  1: basic
  2: application
  3: library
  4: Gradle plugin
Enter selection (default: basic) [1..4] 2

Select implementation language:
  1: C++
  2: Groovy
  3: Java
  4: Kotlin
  5: Scala
  6: Swift
Enter selection (default: Java) [1..6] 3

Split functionality across multiple subprojects?:
  1: no - only one application project
  2: yes - application and library projects
Enter selection (default: no - only one application project) [1..2] 2

Select build script DSL:
  1: Groovy
  2: Kotlin
Enter selection (default: Groovy) [1..2] 1

Project name (default: gradle-multi-proj-setup): gradle-multi-proj-setup
Source package (default: gradle.multi.proj.setup):

> Task :init
Get more help with your project: https://docs.gradle.org/6.7.1/samples/sample_building_java_applications_multi_project.html

BUILD SUCCESSFUL in 1m 4s
2 actionable tasks: 2 executed
jraymond@snappi gradle-multi-proj-setup $ ls -la
total 56
drwxr-xr-x  15 jraymond  staff   480 22 Nov 11:22 .
drwxr-xr-x  20 jraymond  staff   640 22 Nov 11:00 ..
drwxr-xr-x  12 jraymond  staff   384 22 Nov 11:00 .git
-rw-r--r--   1 jraymond  staff   154 22 Nov 11:22 .gitattributes
-rw-r--r--   1 jraymond  staff   382 22 Nov 11:22 .gitignore
drwxr-xr-x   7 jraymond  staff   224 22 Nov 11:22 .gradle
-rw-r--r--   1 jraymond  staff  1931 22 Nov 11:21 README.md
drwxr-xr-x   4 jraymond  staff   128 22 Nov 11:22 app
drwxr-xr-x   4 jraymond  staff   128 22 Nov 11:22 buildSrc
drwxr-xr-x   3 jraymond  staff    96 22 Nov 11:21 gradle
-rwxr-xr-x   1 jraymond  staff  5766 22 Nov 11:21 gradlew
-rw-r--r--   1 jraymond  staff  2763 22 Nov 11:21 gradlew.bat
drwxr-xr-x   4 jraymond  staff   128 22 Nov 11:22 list
-rw-r--r--   1 jraymond  staff   408 22 Nov 11:22 settings.gradle
drwxr-xr-x   4 jraymond  staff   128 22 Nov 11:22 utilities
jraymond@snappi gradle-multi-proj-setup $ tree
.
├── README.md
├── app
│   ├── build.gradle
│   └── src
│       ├── main
│       │   ├── java
│       │   │   └── gradle
│       │   │       └── multi
│       │   │           └── proj
│       │   │               └── setup
│       │   │                   └── app
│       │   │                       ├── App.java
│       │   │                       └── MessageUtils.java
│       │   └── resources
│       └── test
│           ├── java
│           │   └── gradle
│           │       └── multi
│           │           └── proj
│           │               └── setup
│           │                   └── app
│           │                       └── MessageUtilsTest.java
│           └── resources
├── buildSrc
│   ├── build.gradle
│   └── src
│       └── main
│           └── groovy
│               ├── gradle.multi.proj.setup.java-application-conventions.gradle
│               ├── gradle.multi.proj.setup.java-common-conventions.gradle
│               └── gradle.multi.proj.setup.java-library-conventions.gradle
├── gradle
│   └── wrapper
│       ├── gradle-wrapper.jar
│       └── gradle-wrapper.properties
├── gradlew
├── gradlew.bat
├── list
│   ├── build.gradle
│   └── src
│       ├── main
│       │   ├── java
│       │   │   └── gradle
│       │   │       └── multi
│       │   │           └── proj
│       │   │               └── setup
│       │   │                   └── list
│       │   │                       └── LinkedList.java
│       │   └── resources
│       └── test
│           ├── java
│           │   └── gradle
│           │       └── multi
│           │           └── proj
│           │               └── setup
│           │                   └── list
│           │                       └── LinkedListTest.java
│           └── resources
├── settings.gradle
└── utilities
    ├── build.gradle
    └── src
        ├── main
        │   ├── java
        │   │   └── gradle
        │   │       └── multi
        │   │           └── proj
        │   │               └── setup
        │   │                   └── utilities
        │   │                       ├── JoinUtils.java
        │   │                       ├── SplitUtils.java
        │   │                       └── StringUtils.java
        │   └── resources
        └── test
            └── resources

54 directories, 21 files
jraymond@snappi gradle-multi-proj-setup $
```

As we can see, default sub-projects were created.  Those default sub-projects can be replaced with what we need: _service-api_ and _service-client_.  So
we can go ahead and delete the following folders:

`/app`

`/list`

`/utilites`

And create the following empty folders:

`service-api`

`service-client`

We now have:

```shell script
itjraymond $ ls -la
total 72
drwxr-xr-x  14 jraymond  staff   448 22 Nov 11:31 .
drwxr-xr-x  20 jraymond  staff   640 22 Nov 11:00 ..
drwxr-xr-x  12 jraymond  staff   384 22 Nov 11:00 .git
-rw-r--r--   1 jraymond  staff   154 22 Nov 11:22 .gitattributes
-rw-r--r--   1 jraymond  staff   382 22 Nov 11:22 .gitignore
drwxr-xr-x   7 jraymond  staff   224 22 Nov 11:22 .gradle
-rw-r--r--   1 jraymond  staff  9126 22 Nov 11:31 README.md
drwxr-xr-x   4 jraymond  staff   128 22 Nov 11:22 buildSrc
drwxr-xr-x   3 jraymond  staff    96 22 Nov 11:21 gradle
-rwxr-xr-x   1 jraymond  staff  5766 22 Nov 11:21 gradlew
-rw-r--r--   1 jraymond  staff  2763 22 Nov 11:21 gradlew.bat
drwxr-xr-x   2 jraymond  staff    64 22 Nov 11:31 service-api
drwxr-xr-x   2 jraymond  staff    64 22 Nov 11:31 service-client
-rw-r--r--   1 jraymond  staff   408 22 Nov 11:22 settings.gradle

itjraymond $ tree
.
├── README.md
├── buildSrc
│   ├── build.gradle
│   └── src
│       └── main
│           └── groovy
│               ├── gradle.multi.proj.setup.java-application-conventions.gradle
│               ├── gradle.multi.proj.setup.java-common-conventions.gradle
│               └── gradle.multi.proj.setup.java-library-conventions.gradle
├── gradle
│   └── wrapper
│       ├── gradle-wrapper.jar
│       └── gradle-wrapper.properties
├── gradlew
├── gradlew.bat
├── service-api
├── service-client
└── settings.gradle

8 directories, 10 files
```

We need to express those changes (i.e. removal of `/app`, `/list`, `/utilities` and addition of `/service-api` and `/service-client`) and 
that is done withing the `settings.gradle` file.  Before editing the `settings.gradle`, the file content should be as follow:

```shell script
itjraymond $ cat settings.gradle
> rootProject.name = 'gradle-multi-proj-setup'
> include('app', 'list', 'utilities')

itjraymond $
```

We need to edit the file to contain the following:

```shell script
itjraymond $ cat settings.gradle
> rootProject.name = 'gradle-multi-proj-setup'
> include('service-api', 'service-client')

itjraymond $
```

At this point, you should get the following `git status` output:

```shell script
itjraymond $ git status
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   .gitignore
	modified:   README.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	.gitattributes
	buildSrc/
	gradle/
	gradlew
	gradlew.bat
	settings.gradle

no changes added to commit (use "git add" and/or "git commit -a")
```

We can commit this as the first initial project setup.  Note that because `/service-api` and `/service-client` folders are empty, they are not part of this commit.

```shell script

```


We will also need to create a `build.gradle` at the root of the project.  This `build.gradle` will contain build configuration for the multi-project setup
and configuration common for both sub-projects.  But before creating the `build.gradle`, we can create our Spring Boot application 
from [spring initializr](https://start.spring.io/).