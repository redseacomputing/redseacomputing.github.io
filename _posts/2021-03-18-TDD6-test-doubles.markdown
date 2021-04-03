---
layout: post
title:  "TDD for kickstarters- part 6"
date:   2021-03-19 12:00:06 +0100
categories: tdd
permalink: /:year/:title
---

![test doubles in multi-layered architectures](../images/TDD/TDD6-test-doubles.png)

## Advantages of TDD approaches with Test doubles in multi-layered architectures

In my last post we discussed the different approaches of TDD. Unfortunately, it doesn't always stay that simple. 
What if we have external collaborators as dependencies, which are possibly expensive, and above all, of which we do not even know the internals?
For example, if you wanted to develop a network application, how would you get your solution under test control?
We should be able to model the network connection in our main memory. And this is where fakes come into play.

There are various fakes. Today we want to deal with the basic ones. You are working on a module that has 
external dependencies (a network or a database connection for example), which we see as a black box.
We don't want to call these resources over and over again in our tests. 
We are only interested in knowing how our units handle them.

<br>

>Fakes make Dependencies swappable by Dependency Injection

<br>

Let's use an example to illustrate this.

    @Test
    public void donatedMovieAddedToCatalogueWithImdbInfo(){
        String imdbId = "";
        String title = "";
        int year = 2003;
        MovieInfo movieInfo = new FakeMovieInfo(title, year);
        Library library = new Library(movieInfo);
        library.donate(imdbId);
        Movie movie = library.findMovie(imdbId);
        assertEquals(title, movie.getTitle());
        assertEquals(year, movie.getYear());
    }

    public interface MovieInfo {

    }

    class InternetMovieDatabase implements MovieInfo(){ 
        .
        .
        .
    }
    
    class FakeMovieInfo implements MovieInfo() {
        private final String title;
        private final int year;

        public StubMovieInfo(String title, int year) {
            this.title = title;
            this.year = year;
        }
    }

Your test says that you get a movie information from a database and you store it in your internal catalogue/library.
Instead of calling the database, you fake the database information, so you can use this fake object for testing purposes.
The external dependency is a [Separation of Concern](https://en.wikipedia.org/wiki/Separation_of_concerns).

### Outside in design using Stubs and Mocks
#### Stub
A Stub is a test double. It looks like the same from the outside as the origin object, but it has hardcoded information.
All what it does is, that it stores test data.

>Stubs are objects to fetch data from external dependencies and they are returning test data.

#### Mock
Mock objects tests commands of external services like an email server without sending
the mails really.

>Mocks are objects that allows you to test some invoked methods.


### Summary
Fakes simulates dependencies from external packages so your tests stays internal and are from the client side
(Outside In-perspective/Black Box). The real implementation is somewhere else. It is a separate concern,
so you can "Fake it till you make it".


This is the last part of the TDD kickstart beginner series.