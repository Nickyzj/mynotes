[Creating A Test Automation Framework Architecture With Selenium (Step-By-Step)](https://www.youtube.com/watch?v=DO8KVe00kcU)

## Types of automated Testing

* unit testing
* integration testing
* blackbox automated testing (system test, uat, at, etc)

### unit testing

* test the smallest unit of code, in isolation

### integration testing

* tests units together, but still focus on the code

### blackbox automated testing

* from the perspective of the user

## why blackbox automated testing

### regression

* it worked yesterday
* re-test every two weeks

### absolute requirements

* business requirements, pass or fail

### leverage

* BATs test much more production code with fewer lines of BAT code

## common failure points

* recoded tests
* not building a framework
* writing tests like code

## Seperate automation framework

* Tests -> Framework -> Web App

* Simple Tests
* tests drive creation of framework

## architecture

- Tests -> framework -> selenium -> Browser (Web app)
- each layer only interacts with the layer immediately below it

### the page pattern

LoginPage

* login()
* resetPassword()
* ToggleRememberMe()

pages are a good way to model the functionality of an application

## some basic rules (never)

1. never require tests to declare variables, use config file...

   easy to write tests

2. never require test to use the "new" keyword or create new objects

   hard to understand by non-dev people

3. never require the tests to manage state on their own

4. never expose the browser or DOM to the tests or let them manipulate it directly

## some basic rules (alwasy)

1. always reduce the number fo parameters for API calss when possible
2. alwasy use default values instead of requiring paramters when possible

3. use LAST_GENERATED_XXX

## tips

1. automate difficult things
2. errors versus failures
3. Continuous integration, make automated tests part of your build
4. scaling out