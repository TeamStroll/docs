# How to API

Frontend (iPad/website) -> Controller —> Facade —> Domain —> SQL DB

## Overview of the backend:
Bitbucket repository: sh_repo
Ideal IDE: Eclipse
Stroll backend (SBE) is built using a Spring framework and CRUD (Create, Read, Update, Delete) Repositories that deal with an SQL Database. (This means absolutely nothing, so just read on)

## Domain objects
In the sh.platform/src/main/java/com.sh.platform.domain.model directory of the project there are a bunch of packages, each standing for a different type of object that we use. There you’ll find patients, users, facilities, etc. Inside each package, there are usually at least 3 files:

1. `<domain object name>.java (domain object)`
2. `<domain object name>Factory.java (factory)`
3. `<domain object name>Repository.java (repository)`

Think of the domain object as a plain-old java objects that store information and nothing else. They have a list of fields and getters and setters for those fields. No actual computation is done in these objects. Each domain object has an associated SQL table whose columns are the fields of that object.
The factories are responsible for creating these domain objects. Instead of instantiating a new domain object like Question as Question question = new Question(), we use QuestionFactory to say Question question = questionFactory.makeQuestion(). 
The repositories are interfaces that actually save the data in the SQL database. Each repository extends what is called a CrudRepository which has a super function called save() which will put an instance of the domain object into the SQL database. Repositories also deal with creating queries to a particular table.

### An example:

```java
	Question newQuestion = questionFactory.makeQuestion(<parameters>);
	questionRepository.save(newQuestion);
```

This example literally just creates a new question and saves it into the database in just 2 lines of code. Pretty nifty, huh?

## Controllers and SHFacade:
Ok, so now that we have somewhat an understanding of the domain, where the **** would the example code above even go?
As illustrated on the first line, information is passed from the front-ends to the Controller. The Controller files are found in com.sh.platform.interfaces.mvc. SHController.java has the most general API calls in it. The way the front-ends call the controllers is by using an HTTP POST/GET to the base url of sbe.cloudapp.net:80/sh. To call a specific API, you must append the end of the base url with whatever is found in the @RequestMapping value above the function. 
Essentially the role of the Controller is to parse the url, convert the request data in the form of Data-Transfer-Objects (DTOs) to domain objects, and then pass them along to the SHFacade where actual domain-object manipulation occurs. 
In SHFacade, you no longer deal with DTOs and you can deal with the domain. 

### Creating a new API call:
If you need to create a new API call that does not require a new object, then skip to “Adding to SHController and SHFacade”. If you do need to create a new object, let’s get started:

### Creating domain objects:
To create a new domain object, you can make a new package for it and follow the templates of the object, factory, and repositories given in any other package. DO NOT FORGET ANNOTATIONS (the things with @ in front of them). I suggest the copy-paste-manipulate framework personally ;). Do not worry about creating an SQL table before creating the domain object, that will happen automatically once you run the program. 

### Creating DTOs:
Next, create the DTOs needed. If you are trying to send a list of domain objects inside of one object, you need to create a DTO for the singleton object, and then a DTO to hold the array of singleton DTOs (see QuestionDTO and QuestionsDTO if you are confused). Also create their assemblers. DO NOT FORGET ANNOTATIONS.

## Adding to SHController and SHFacade:
First let’s add to SHController. You will need to think of a new url at which your API could be called. Follow the template given for each other API call. DO NOT FORGET ANNOTATIONS (have I said this??). Also, don’t forget to specify the request type, be it GET, POST, or (rarely) PUT. Be sure to import any objects you may have created in the previous steps and @Autowire instances of your repositories and factories. 
Once you’ve made your own request mapping and such, if applicable, de-assemble DTOs into domain objects, and pass them on to SHFacade.
In SHFacade, write your function using domain objects. Here it might be useful to use a new object called a service. These are much like the Factories and Repositories in that each domain object has a <domain object name>Service.java associated with it if it needs. Look at other examples to see if you need it. 
If no domain objects are required, feel free to do most of the manipulation directly in SHController (bypass SHFacade), but the whole function should not take more than 20 lines or so. If it does, consider using SHFacade. 
