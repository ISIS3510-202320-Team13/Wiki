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
One of the BQs for the past sprint included checking the users location every so often to see if their location matches that of the parking lot that they are making a reservation for.

To solve this, a coroutine whose job was to check the users location was implemented as soon as a user makes a reservation.

When looking at the profiling tool, we can see that this coroutine is peaking the CPU usage when it wakes up.

![image](https://github.com/ISIS3510-202320-Team13/Wiki/assets/57652524/29ac8bd0-d1ea-447f-87b7-85b00d0f1ccf)


#### Optimization Implementation
We identified that the coroutine was checking for location permissions each time that it checks the user location.

This is unnessary because the permissions should only be checked once when the view is created, and if they are granted, they shouldn't be checked again.

```kotlin
    override fun onViewCreated(view: View, savedInstanceState: Bundle?) {

        super.onViewCreated(view, savedInstanceState)
        checkLocationPermissions()
        ...
}
```
This check was removed from the coroutines function, so now the thread only needs to calculate the distance to the parking lot every so often.

```kotlin
    private fun getCurrentUserCoordinates() {
        viewModel.parkingDetailLiveData.observe(viewLifecycleOwner) { parkingDetail ->
            parkingDetail?.let {
                val parkingAddress = parkingDetail.coordinates
                    getCurrentLocation { location ->
                        location?.let {
                            val userCoord = LatLng(location.latitude, location.longitude)
                            if (parkingAddress != null) {
                                if (abs(userCoord.latitude) == abs(parkingAddress.latitude) && abs(
                                        userCoord.longitude
                                    ) == abs(parkingAddress.longitude)
                                ) {
                                    matchCoord++
                                }
                            }
                        }
                    }
            }
        }
    }
```

#### After Optimization
This way, the CPU usage is reduced by 5% than what it was before

![image](https://github.com/ISIS3510-202320-Team13/Wiki/assets/57652524/a47a0af6-9e7d-4b3c-84fb-c20ab3359218)

#### Before optimization

The binding was initialized in the onCreateView function using lateinit which can generate unpredictable behaviour and race conditions. In order to avoid these issues the binding variable was initialized in its declaration and using the "lazy" properties. The lazy manager is thread-safe by default, ensuring that multiple threads attempting to access the property in parallel will wait for initialization to complete and share the same initialization value.

#### After Optimization

Binding initialization only occurs the first time the property is accessed.
![image](https://github.com/ISIS3510-202320-Team13/Wiki/assets/69486519/a1ecff35-a536-46d7-963c-871236cac8db)


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
-**GPS**: A map is displayed on the user location and showing the parkings stored on the database.

#### Sprint 3 Features
- **Show Different Parkings Stored on the Database**: Displays various parking options available in the database.
- **Make a Reservation**: Enables users to reserve parking spots through the app.
- **Confirmation Email**: Sends confirmation emails to users upon successful reservation.
- **Show Parking Details**
- **Allows payments with stripe api**
- **Generate recipe and show details to the user**
#### Sprint 4 Features
- **Show Reservation History**: Allows users to view their past parking reservations.
- **Retrieve and Show User Information**: Displays user's personal information on a dedicated view.
- **Allow User Log Out**: Provides the functionality for users to securely log out of the app.
- **Allow the user to cancell reservation**: Gives the user the option to cancell an ongoing reservation.
- **Send user confirmation Email**: The user gets a email confirmation with its reservation
  

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
- Are the parking spots loading in less than 3 seconds (on devices with Android version 8.0 or higher) or do we have to change something to achieve this? (performance) (Sebastian Caceres)
- How many times per reserve is the user location matching the parking location? (update - Prehold a spot for a certain amountof time) (Nicolas Falla)
- How much time it takes to reserve a parking spot? Is it possible to reduce unnecessary steps? (Juan Camilo)
- What are is most reserved parking spots by a user in each day of the week? (Cristóbal Arroyo)
- Does the user have a currently active or upcoming reservation? (Juan Diego Lugo)
- What are the user last reserved parking spots? (Sergio Peñuela)

#### Sprint 4 BQs
- The app is fetching the reservations of the user and displaying in less of three seconds? (Improve user experience)
- Which is the last reservation made by an user? (Improve user experience)
- How much time does it take for a user to fill in the payment method? (new feature - be able to save credit card information)
- Can the user see the reservation without having the app? (Improve user experience)
- How much time does a user take to fill in the start time and end time for a new reservation?

### c. Eventual Connectivity Strategies 
- **App Continuation During Disconnection**: The app continues to display some of the parking spots stored in the cache when disconnected.
- **Reservation Continuity**: The app allows users to continue making a reservation during intermittent connectivity, showing an error only upon confirmation if disconnected.
- **Cancell reservation**: The app will notify the user of the innability to cancell a reservation beacause of the lack of connectivity.

### d. Local Storage Strategies 
- **Reservation Data Storage**: Stores the latest reservation data in local files for offline access to upcoming reservations.
- **Saving User Basic information in local storage** : Stores the user image, email and name of the user locally to retrieve it when the app is offline.
- **Store information for QR**: Stores the information to show the user its last reservation and for QR to activate its reservation

### e. Multi-threading Strategies
- **Efficient Data Fetching**: Uses threads and async operations for efficient data fetching from the database, it is ysed when the reservations of the used are fetched.
- **App Telemetry**: Use threads and async operations for calculating performance metrics inside the application
- **New API calls**: Usage of Future Async functions to do some tasks

### f. Caching Strategies
- **Parking Spot Caching**: Caches nearby parking spots to load them faster during reconnection or app restarts.
- **GPS Data Caching**: Minimizes repeated GPS usage by caching and sharing location data between views.
- **Save Reservations History** : Caching the last 3 reservations when the app is offline, this allows the user to know the latest reservations even when the app has no internet access.



**Ethics:** 
https://youtu.be/G5zVMSiB18o



[Back to Home](../README.md)
