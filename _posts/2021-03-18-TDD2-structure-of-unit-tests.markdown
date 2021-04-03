---
layout: post
title:  "TDD for kickstarters- part 2"
date:   2021-03-19 12:00:02 +0100
categories: tdd java
permalink: /:year/:title
---

![structure of an unit test](../images/TDD/TDD2-structure-of-unit-tests.png)

# The structure of a test

Every unit test contain at least three parts:

#### Arrange
Arrange gets everything ready to perform the test. 
This could be declaring variables, building required objects or 
setting the state of a unit based on the circumstances you want to 
test.

#### Act
Act performs the action that you are testing on the unit.

#### Assert
Assert checks to see that the action performed correctly. You want to check that 
either the return value of a method call is expected, or the state of an object is as expected.

    @Test
    public void thisTestShouldBeStructured(){
        //Arrange
        Student student = new Student("John Doe");
        //Act
        student.setName("Jane Doe");
        //Assert
        assertEquals("Jane Doe", student.getName());
    }


## Hints
Here are 3 hints for effectiveness and sustainability.
Let's use a DVD-library example.

### Hint 1: Don't make the set up first. Start with the assertion in the tests.
#### Ask the question first: <br>
Is the movie in the catalogue of the library?



    @Test
    public void donateMovie(){
        assertTrue(library.getCatalogue().contains(movie));
    }



#### Working back from the setup that asks the question: <br>
  
Okay, you need a library here, so lets declare it.


    @Test
    public void donateMovie(){
        Library library;
        assertTrue(library.getCatalogue().contains(movie));    
    }

Create the production class Library with IDE from your test case.



    public class Library {
    
    }



Okay, you have to implement the method getCatalogue() from your test case.


    public class Library {
    
        public Collection<Movie> getCatalogue() {
            return null;
        }
    }

Create the production class Movie with IDE from test case and maintain your test specification.


    @Test
    void donateMovie() {
        Library library = new Library();
        Movie movie = new Movie();
        assertEquals(true, library.getCatalogue().contains(movie));
    }


Now it comes to an action in your test. You have to add it on the library with a namefull method.


    @Test
    void donateMovie() {
        Library library = new Library();
        Movie movie = new Movie();
        library.donate(movie);
        assertEquals(true, library.getCatalogue().contains(movie));
    }


And you have to declare that method donate(Movie movie) with the IDE again in your production code.


    public class Library {
    
        public Collection<Movie> getCatalogue() {
            return null;
        }
    
        public void donate(Movie movie) {
    
        }
    }


You are referencing things that don't exist yet, and then you're working your way backwards
from the references to the declaration.
The reference come first and this is very much the essence of test driven development.
You **refer to things** in a test and that forces you to declare it. Therefore, it is **test driven** in a very strict way.
And that means that you end up with the exact set up, that you need to ask the question that you want to ask.

Sometimes I have written the set up and then got to write the assertion where
I thought: "Oh, I havent actually that what I need to make the assertion".

So you have to work backwards from the assertion.
It is all about the question you want to ask and this is the most important thing about the test.

>Its mentally a good way from a design point of view to start from the WHAT (here is the question) working backwards to the HOW (here is the implementation).

### Hint 2: See your test fail

Some teams got 100 percent test coverage, because it is clear.
Important is here, not to write just 100 percent test coverage with dumbass assertTrue's.
It is important to write the right tests (with meaningful and the right questions) **and** check that they are failing.

If you would run the test from this example it would fail. But lets look why is it failing.
It's failing because of a NullPointerException.
You are trying to check if an object is in a collection that's actually null.

What you really want to know (at exactly this point) is: If the results of this test are wrong, would this test fail?
You dont want to see it fail because of some unhandled exception or something else. You want to see exactly what happens if the
donated movie is not in the catalogue.

So for now let's just return an empty ArrayList.

    public class Library {
    
        public Collection<Movie> getCatalogue() {
            return new ArrayList<>();
        }
    
        public void donate(Movie movie) {
    
        }
    }

When you are run the test again, the test result is saying you now an Assertion-Error. So thats the point of hint 2:

Before you write the code to pass the test, **see the test fail**.
**You are testing your test** before you make it pass

You can go forward and have confidence in your unit tests. If someone works on it in the future,
this test would immediately indicate that something was going in the wrong direction.

As a conclusion of the first two chapters:
Experienced programmers criticized test suites with passing tests, but the production code was hopelessly broken.
If you are asking high quality questions and check your own tests, you have more confidence in your unit tests, and 
they are going forward as regression tests too.

The interested reader is invited to let the test pass.

When you are looking at your test suite now, there is a little code smell. You find here a so called message chain.
That's when you're navigating through a relationship to one object to the next object in the chain.
This breaks a principle called "The law of demeter".

In this case you have unencapsulated this list in your assertion. Your client code knows that it's a collection
and that's a little messy. We like encapsulation and are big fans of it.<br>
So lets encapsulate this:<br> 
Extract a method of it and call it contains() and move it to the Library class.

Rerun your tests as soon as your refactoring.

#### Next requirement

We register at least one copy of the movie with every movie that's added to the library.
Let's think about the specification/test and implement it:


    @Test
    void donateMovie() {
        Library library = new Library();
        Movie movie = new Movie();
        library.donate(movie);
        assertEquals(true, library.contains(movie));
        assertEquals(1, movie.getCopies();
    }

### Hint 3: Test one thing per test

The next refactoring should be done. What's really wrong with your production code, if the test fails?
Every test should do just one thing, so create a separate one and let it run.

    public class DonateMovieTest {
    
        private final Library library;
        private final Movie movie;
    
        public DonateMovieTest() {
            library = new Library();
            movie = new Movie();
        }
    
        @Test
        void donateMovie() {
            library.donate(movie);
            assertEquals(true, library.contains(movie));
        }
    
        @Test
        void rentalCopyAdded() {
            library.donate(movie);
            assertEquals(1, movie.getCopies());
        }
    
    }


Perhaps everyone will now say that this is far too expensive for so little code.
Because the advantages tend to emerge in the long term: <br>
>By constantly refactoring in small steps, you get a maintainable
product that is readable and therefore more cost-effective.

This is part two of the TDD kickstart beginner series. Here is [part 3](https://redseacomputing.github.io/2021/TDD3-preparation-of-tests)
