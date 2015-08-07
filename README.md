You'll need this repository:

```
  <repositories>
    <repository>
        <id>s3-releases</id>
        <url>http://sillelien-maven-repo.s3-website-eu-west-1.amazonaws.com/release</url>
    </repository>
</repositories>
```

And the maven co-ordinates are:

```
    <dependency>
        <groupId>com.github.sillelien</groupId>
        <artifactId>dollar-core</artifactId>
        <version>0.1.65</version>
    </dependency>
```

An example of a project using this is [Tutum API](https://github.com/sillelien/tutum-api) which is very much a work in progress.

## FAQ

### Why Dollar ?

Once you've written some Dollar code you'll get the reason pretty quickly.

### Is this like jQuery for Java?

No, but Dollar uses a lot of ideas that jQuery popularized, so I would certainly acknowledge our debt to jQuery.

### Then what is it?

If you like the ease of JavaScript, Ruby, Groovy etc. but also enjoy being able to work within the Java language then this is for you. You can write typesafe code and then drop into typeless Dollar code whenever you need to. Dollar is both an alternative paradigm and a complementary resource.


## Examples

### Basic

You can just use dollar to write dynamic JSON oriented (JSON is not a requirement, you can work with maps too) using a fluent format like this:

        int age = new Date().getYear() + 1900 - 1970;
        var profile = $("name", "Neil")
                .$("age", age)
                .$("gender", "male")
                .$("projects", ("snapito", "dollar"))
                .$("location",
                        $("city", "brighton")
                                .$("postcode", "bn1 6jj")
                                .$("number", 343)
                );

or using a more builder format like this:

        var profile = $(
                $("name", "Neil"),
                $("age", new Date().getYear() + 1900 - 1970),
                $("gender", "male"),
                $("projects", ("snapito", "dollar")),
                $("location",
                        $("city", "brighton"),
                        $("postcode", "bn1 6jj"),
                        $("number", 343)
                ));

and these hold true:

        assertEquals(age /11, (int)profile.$("$['age']/11").());
        assertEquals("male", profile.$("$.gender").$());
        assertEquals(10, profile.$("5*2").$());
        assertEquals(10, (int)("10").());
        assertEquals($("{\"name\":\"Dave\"}").$("name").$$(),"Dave");
        assertEquals($().$("({name:'Dave'})").$("name").$$(), "Dave");


## Characteristics

Dollar is designed for production, it is designed for code you are going to have to fix. Every library and language has it's sweet spot. Dollar's sweetspot is working with schema-less data in a production environment. It is not designed for high performance systems (there is a 99.9% chance your project isn't a high performance system) but there is no reason to expect it to be slow either. Where possible the code has been written with JVM optimization in mind.

With this in mind the following are Dollar's characteristics:

* Simple - Dollar does do not expose unnecessary complexity to the programmer, we keep it hidden.

    > The secret of success is to be like a duck – smooth and unruffled on top, but paddling furiously underneath.”

* Typeless - if you *need* strongly typed code stop reading now. If you're writing internet centric modest sized software this is unlikely to be the case.
* Synchronous - asynchronous flows are hard to follow and even harder to debug in production. We do not expose asynchronous behaviour to the programmer.
* Metered - key execution's are metered using Coda Hale's metrics library, this makes production monitoring and debugging easier.
* Nullsafe - Special null type reduces null pointer exceptions, which can be replaced by an isNull() check.
* Threadsafe - No shared state, always copy on write. No shared state means avoidance of synchronization primitives, reduces memory leaks and generally leaves you feeling happier. It comes at a cost (object creation) but that cost is an acceptable cost as far as Dollar is concerned.

## The Rules

1. Do not create your own Threads.
2. Do not create your own Threads.
3. Always run from a *static* context (e.g. a public static void main method)
4. All `var` objects are **immutable**, so use the returned value after 'mutation' actions.


## Badges
Build Status: [![Circle CI](https://circleci.com/gh/sillelien/dollar-core.svg?style=svg)](https://circleci.com/gh/sillelien/dollar-core)

Chat: [![Gitter](https://badges.gitter.im/Join Chat.svg)](https://gitter.im/sillelien/dollar-core?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)

Waffle Stories: [![Stories in Ready](https://badge.waffle.io/sillelien/dollar-core.png?label=ready&title=Ready)](https://waffle.io/sillelien/dollar-core)

Dependencies: [![Dependency Status](https://www.versioneye.com/user/projects/55bf9094653762001a002527/badge.svg?style=flat)](https://www.versioneye.com/user/projects/55bf9094653762001a002527)

