# Sprint 4

**Team 13**


## Table of Contents Sprint 4

1. [Value Proposition](#1-value-proposition)
2. [Micro-Optimization Strategies](#2-micro-optimization-strategies)
3. [Implementation of New Features](#3-implementation-of-new-features)
4. [Development of New Views](#4-development-of-new-views)
5. [Implementation of New Business Questions (BQ)](#5-implementation-of-new-business-questions-bq)
6. [Comprehensive Listing and Description](#6-comprehensive-listing-and-description)
7. [Additional Competences](#7-additional-competences)

## 1. Value Proposition

ParkEz, a pioneering mobile application, is reshaping the urban parking landscape in Bogotá by seamlessly connecting parking seekers with a wide array of parking options. At its core, ParkEz is designed to alleviate the common frustrations associated with urban parking. It provides real-time updates on parking availability, an advanced search feature with various filters, and a streamlined reservation and payment system. The application stands out with its user-centric approach, offering personalized parking recommendations based on individual user behavior and preferences. Additionally, ParkEz’s integration of micro-optimization, multi-threading strategies, and local storage and caching mechanisms ensures a smooth and responsive user experience, even in low connectivity areas.

ParkEz extends its value beyond mere convenience for its users. It serves as a vital tool for parking space owners, enhancing their visibility and customer reach, thereby opening new avenues for revenue generation. This innovative platform not only simplifies the process of finding and booking parking spaces but also contributes to a more sustainable urban environment. By reducing the time and resources spent in search of parking, ParkEz aids in decreasing fuel consumption and emissions, aligning with the broader goals of urban sustainability and efficiency.
## 2. Micro-Optimization Strategies

### 3.1  Kotlin App Profiling and Optimization

#### Before Optimization
- **Screenshot and Analysis**: 

#### Optimization Implementation
- **Code Snippets/Descriptions**: 

#### After Optimization
- **Screenshot and Analysis**:

### 3.2 Flutter App Profiling and Optimization

#### Before Optimization

One of the main features of the App is track user's location and find near parkings.

Currently, the App is updating the internal `Position` variable whenever the GPS has a location change.

With dart DevToools, it's clear that this feature is the most CPU consuming:

![before-optimization](https://github.com/ISIS3510-202320-Team13/Wiki/assets/69475004/39655dc8-2397-4af4-a64a-c7d3460b9a3e)

#### Optimization Implementation
We use `Geolocator` library to track user's position. 

`LocationBloc` class uses a `StreamSubscription` to get position changes.

```dart
class LocationBloc extends Bloc<LocationEvent, LocationState> {
  late final StreamSubscription _locationSubscription;

  LocationBloc() {
    _locationSubscription = Geolocator.getPositionStream().listen(
      (position) => add(LocationUpdated(position)),
    );
  }

  ...
}
```

The problem with this approach is that `getPositionStream()` method, defaults the streaming rate to notify all GPS movements.

Reading [geolocator API reference](https://pub.dev/documentation/geolocator/latest/#listen-to-location-updates):
> `distanceFilter`: the minimum distance (measured in meters) a device must move horizontally before an update event is generated;
 
Then, the obvious solution is that we should change the distanceFilter so that the updates are only done when the user moves a great distance:

```dart
class LocationBloc extends Bloc<LocationEvent, LocationState> {
  late final StreamSubscription _locationSubscription;

  LocationBloc() {
    _locationSubscription = Geolocator.getPositionStream(
            locationSettings: const LocationSettings(distanceFilter: 20)) // ADDED DISTANCE FILTER OPTION
        .listen(
      (position) => add(LocationUpdated(position)),
    );
  }

  ...
}
```


#### After Optimization

After applying the optimization, the Location feature isn't the one that consumes the most CPU, and if we filter out the rest of the tasks, we can see that it improved the runtime inside the App from 41.56ms to 18.06, almost 3 times faster!

![after-optimization](https://github.com/ISIS3510-202320-Team13/Wiki/assets/69475004/6113aaa1-7aa8-45b1-9bcc-aff3aa372a68)


### Summary of Optimizations


## 3. Comprehensive Listing and Description
### a. Features Delivered

#### Sprint 2 Features
- **Real-Time Location with GPS**: Provides real-time location tracking using the phone's GPS.
- **Answering Type 2 Questions**: Addresses questions related to parking reservations, history, and recommendations.
- **Context-Aware Dark Mode**: Adapts the app's appearance based on ambient light conditions.
- **Smart Feature - Personalized Recommendations**: Offers parking recommendations based on user behavior.
- **User Authentication**: For secure access and personalized features.
- **External Service Integration - Firebase User Registration**: Manages user data and authentication securely.

#### Sprint 3 Features
- **Show Different Parkings Stored on the Database**: Displays various parking options available in the database.
- **Make a Reservation**: Enables users to reserve parking spots through the app.
- **Display the Most Used Parkings**: Highlights parking spots that are frequently used.
- **Confirmation Email**: Sends confirmation emails to users upon successful reservation.

#### Sprint 4 Features
- **Show Reservation History**: Allows users to view their past parking reservations.
- **Retrieve and Show User Information**: Displays user's personal information on a dedicated view when logged in.
- **Allow User Log Out**: Provides the functionality for users to securely log out of the app.
- **Payments with Stripe**: Integrates Stripe for secure and convenient payment processing.

### b. Business Questions (BQs)

#### Sprint 2 BQs
- At what time is a parking occupied the most/least? (improve user experience)
- How much time does it take for an user to reserve a parking spot? (improving user experience)
- What are the user's most recent actions, so we can save time the next time they want to make a reservation? (improving daily usage/interaction)
- What are the nearest parking locations to the user's most frequented places? (improving daily usage/interaction)
- What is the average waiting time for a parking spot to be freed? (improving experience)

- What parking spots are the most requested in the city? (understand where is a business necessity)
- What is the average/maximum price a user would pay for reserving a parking spot? (understand what is the optimal range of prices and if could be dinamic)

#### Sprint 3 BQs
- At what time is a parking occupied the most/least?  (improve user experience)
- How much time does it take for an user to reserve a parking spot? (improving user experience)
- What are the user's most recent actions, so we can save time the next time they want to make a reservation?  (improving daily usage/interaction)
- What are the nearest parking locations to the user's most frequented places? (improving daily usage/interaction)
- What is the average waiting time for a parking spot to be freed? (improving experience)


#### Sprint 4 BQs
-
-
-
-
-

### c. Eventual Connectivity Strategies 
- **App Continuation During Disconnection**: The app continues to display some of the parking spots stored in the cache when disconnected.
- **Reservation Continuity**: The app allows users to continue making a reservation during intermittent connectivity, showing an error only upon confirmation if disconnected.

### d. Local Storage Strategies 
- **Reservation Data Storage**: Stores the latest reservation data in local files for offline access to upcoming reservations.

### e. Multi-threading Strategies
- **Efficient Data Fetching**: Uses threads and async operations for efficient data fetching from the database.
- **App Telemetry**: Use threads and async operations for calculating performance metrics inside the application

### f. Caching Strategies
- **Parking Spot Caching**: Caches nearby parking spots to load them faster during reconnection or app restarts.
- **GPS Data Caching**: Minimizes repeated GPS usage by caching and sharing location data between views.



[Back to Home](../README.md)
