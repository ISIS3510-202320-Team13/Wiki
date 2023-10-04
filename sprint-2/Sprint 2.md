# Sprint 2

**Table of Contents Sprint 2**
1. [List of business questions](#1-list-of-business-questions)
2. [Implemented functionalities](#2-implemented-functionalities)
3. [Analytics stack or pipeline](#3-analytics-stack-or-pipeline)
4. [Architectural design](#4-architectural-design)
5. [Rationale of architectural design](#5-rationale-of-architectural-design)
6. [Implementation of AD](#6-implementation-of-architectural-design)
7. [Implementation of BQs](#7-implementation-of-business-questions)
8. [Views](#8-views)
9. [Back to Home](../README.md)

## 1. List of business questions.
The BQs (Business Questions) that were implemented are:

Type 2.1 - Calculate the time it takes from when the app is opened (how long a reservation takes).<br />
Type 2.2 - Maintain a history of actions (confirmed reservations, canceled reservations, recurrent reservations).<br />
Type 2.3 - Determine the nearest parking locations to the users' most frequented places (improving daily usage/interaction). We may be able to access this information through the Google Maps API, recommending frequent parking spots in case they are full.<br />
Type 2.4 - Calculate the average waiting time for a parking spot to become available (improving the user experience). This can be calculated from reservation times.<br />
Type 2.5 - What are the nearest parking from the users' most frequented places? (improving daily usage/interaction)<br />Type 2.5 - What are the nearest parking from the users' most frequented places? (improving daily usage/interaction)<br />
Type 2.6 - What is the average waiting time for a parking spot to be freed? (improving experience)<br />

[Back to top](/sprint-2/Sprint%202.md#sprint-2)

## 2.  Implemented functionalities.
a. Real-Time Location with GPS: This functionality utilizes the phone's GPS sensor to provide real-time location tracking. It allows users to see their current location on a map within the app, making it easier to find nearby parking spots or navigate to their destination.

b. Answering Type 2 Questions: As mentioned earlier, this functionality addresses Type 2 questions related to parking reservations, history, and recommendations. It provides answers to questions such as reservation duration, reservation history, and recommends nearby parking spots based on user preferences.

c. Context-Aware Dark Mode: This functionality adapts the app's appearance based on the time of day or ambient light conditions. For example, it switches to a dark mode at night or when the device's brightness is lowered, providing a more comfortable viewing experience in low-light situations.

d. Smart Feature - Personalized Recommendations: This feature employs smart algorithms to analyze user behavior and preferences. It can recommend parking spots based on historical usage patterns, suggesting the most frequently used parking locations or notifying the user when a preferred spot becomes available.

e. User Authentication: User authentication is essential for security and personalization. Users can create accounts, log in, and access personalized features such as saving favorite parking locations and viewing reservation history. This authentication is connected to the backend for data security.

f. External Service Integration - Firebase User Registration: This functionality integrates with an external service, specifically Firebase, for user registration. When users create accounts or log in, their authentication and registration data are securely managed on Firebase servers, ensuring data consistency and security across devices and platforms.
[Back to top](/sprint-2/Sprint%202.md#sprint-2)

## 3.  Analytics stack or pipeline.

For the Analytics Pipeline, we chose Firebase, as it is the most used backend platform for Mobile Applications.

Currently, we're usign Firebase Authentication to save all the users in our App and get all the information from them.
We will also use Cloud firestore to save all the users' reservations and actions with the users.

Specifically for the analytics service, Google Analytics for Firebase will help us process all the events in the App and the user events and show them in Firebase Dashboard to get insigut of all the information we're processing.

![AnalyticsPipeline](https://github.com/ISIS3510-202320-Team13/Wiki/assets/69475004/f0b2e526-3b5c-43ef-9315-886373b22e64)

[Back to top](/sprint-2/Sprint%202.md#sprint-2)

## 4. Architectural design.

![Moviles](https://github.com/ISIS3510-202320-Team13/Wiki/assets/89409633/78d1e05a-2ca5-4fea-9197-daba88e96aea)

The implemented ModelviewModel pattern have  the view module that implements the next views and routes:

![269474086-173ca1da-8f4d-4a84-bd82-bca9df4b7560](https://github.com/ISIS3510-202320-Team13/Wiki/assets/89409633/fe681928-761f-4ef6-a40a-05b930b5e5db)

[Back to top](/sprint-2/Sprint%202.md#sprint-2)

## 5. Rationale of architectural design.

[Back to top](/sprint-2/Sprint%202.md#sprint-2)

## 6. Implementation of architectural design.

[Back to top](/sprint-2/Sprint%202.md#sprint-2)

## 7. Implementation of business questions.

[Back to top](/sprint-2/Sprint%202.md#sprint-2)

## 8. Views

[Back to top](/sprint-2/Sprint%202.md#sprint-2)


