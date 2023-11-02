# Sprint 3

**Table of Contents Sprint 3**

1. [Description of the eventual connectivity scenarios](#1-description-of-the-eventual-connectivity-scenarios)
2. [ List all the functionalities and design details that you implemented](#2-list-of-all-the-functionalities-and-design-details)



## 1. Description of the eventual connectivity scenarios:
The main strategy that we will implement in the app will be Network falling back to cache and Cache then network with the next scenarios:

a. Usage of Cache for Last Reservation Data: When a user makes a reservation, the app should save the reservation data in the cache. If the connection is lost during this process, the app will continue to function by displaying the last saved reservation data. This ensures that users can still access their reservation details even when there is no network connectivity.

b. Usage of Cache for User Email During Login: During the login process, the user's email is crucial for authentication. If there is an issue while filling in the login details (e.g., network disruption), the app should save the partially entered email in the cache. This way, the user can resume the login process without starting from scratch once the connection is re-established.

c. Display Cached Parking Data When Connection is Lost: When the app is fetching parking information from the database, it should save this data in the cache. If the connection is lost, the app will continue to display the parkings stored in the cache. This ensures that users can still browse and access parking information even when they have no network connectivity.

Moreover, you should describe your eventual connectivity 
scenarios and show how the app behaves on them (This is evaluated in the Wiki)


## 2. List all the functionalities and design details that you implemented:
a. List all the features that you will deliver in this sprint (including those that 
you already had in Sprint 2):
* Login functionality
* Sign Up Functionality
* Show the different parkings stored on the database
* Make a reservation
* Display the most used parkings

b. Specify what are your BQs for this sprint.
* Are the parking spots loading in less than 3 seconds (on devices with Android version 8.0 or higher) or do we have to change something to achieve this? (performance) (Sebastian Caceres)

c. Specify what is your eventual connectivity strategy(ies).
d. Specify what is your local storage strategy(ies).
e. Specify what is your multi-threading strategy(ies).
* Usage of threads and async for the fetching of information in the database. 
     

f. Specify what is your caching strategy(ies).
