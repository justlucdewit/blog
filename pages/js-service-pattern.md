<a class="medium-link" href="https://medium.com/@lukedev_/the-javascript-serivce-design-pattern-d819e1137bed">Read on medium</a>

# The Javascript service design pattern

<br />

## Problem: Unorganized API calls
When you’re working on a full-stack web application that communicates with its backend using multiple endpoints. You often do calls through the fetch API or using a library like Axios. Which ends you up with a lot of different Axios or fetch() calls all over your codebase.

One of the ways to clean this up is by making use of a design pattern named ‘services’. This design pattern is used to organize and centralize these API calls in an abstracted module, which means it's very easy to reuse the same calls (possibly with different parameters) in multiple places without having to copy and paste the underlying code.

<br />

## Generic ApiService module
Lets now look at a very simple setup to utilize this technique in your next project using the axios.js library:

<br />
<script src="https://gist.github.com/justlucdewit/b3b467e4fea43e9d279775b13c562fc0.js"></script>

As you can see, this javascript module is called the ApiService, and is designed to be used as a generic wrapper around functionalities for doing GET and POST requests. It will thus be used as the base for every other service you will make later on (including the example later on in this article).

We start off by simply importing the Axios library (a library for doing AJAX web requests), and then determine what API URL to use based on if we are in the production environment or developing locally.

We then create the ApiService object which we then export later on. This ApiService contains 2 properties which are a function to do GET requests, and a function to do POST requests (if you need other methods like DELETE, you could of course use the same technique to add a delete() method to this object).

<br />

## StudentService example
Now let's see how to actually implement a custom service that uses the ApiService to pull and update data from our own API.

<br />
<script src="https://gist.github.com/justlucdewit/463c81698ed4e224a3a4060aedaa10de.js"></script>

In the snippet above, you can now clearly see that this service design pattern can help organize your endpoints and centralize them in one single place, allowing for reusability and abstraction.

All we do is create an object which will be our service, and give it some methods that allow us to do certain actions like creating a new student, getting a list of students, and getting a grade list of a specific student.

All we have to do is determine what parameters the function needs, the endpoint path to the ApiService, together with the parameters in the form of query parameters, route parameters, request body, or anything you want.

Now no matter where we are in your codebase when we want to get a list of all students, we can simply import the student service and simply call <br /> `await StudentService.getAllStudents();` and voila!

<br />

## Advantages

The major advantage that this design pattern offers, and the reason why you probably do wanna be using this technique is the fact that it abstracts the logic of the individual API endpoints, but also abstracts the way we do the API calls themselves.

Let's say that we want to add some form of token authentication to our application, meaning each request will need to carry the token in the request headers.

Now, instead of looking through our entire codebase, and searching for all the places where we used Axios calls, we can simply put this logic within our ApiService, meaning we will only have to update 2 methods in 1 single object to enable authentication for our entire application.

The same thing goes for when you want to change a certain API endpoint, for example, if you want to change the GET api/students` route to GET api/students/all`, you could simply edit the path in the StudentService instead of every single place you called that endpoint.

<br />

## Conclusion

Personally, I'm not one of those people that passionately uses, and brainlessly knows dozens of design patterns, Id like to look at issues in software development in a way that includes the context, meaning. Sometimes an issue that is usually solved using design pattern X, could be better solved in another way depending on the context.

However, regardless of that fact, there is still a lot to learn and understand by looking at the way other people tackle certain issues and set up their codebase. That is why even tho this design pattern might make your project’s codebase easier to work with, it's still important to think about what other things you can use to solve the same issues, and in what way you can tweak this pattern to better fit your use-case.

In other words: you’re better off using a design pattern as a loose guide, rather than a strict copy/paste way of doing things.