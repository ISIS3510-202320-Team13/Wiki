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
9. [Views](#9-Videdo Ethics)
10. [Back to Home](../README.md)
11. 

## 1. List of business questions.
The BQs (Business Questions) that were implemented are:

#### Type 2
1. At what time is a parking occupied the most/least?  (improve user experience)
2. How much time does it take for an user to reserve a parking spot? (improving user experience)
3. What are the user's most recent actions, so we can save time the next time they want to make a reservation?  (improving daily usage/interaction)
4. What are the nearest parking locations to the user's most frequented places? (improving daily usage/interaction)
5. What is the average waiting time for a parking spot to be freed? (improving experience)

#### Type 4
1. What parking spots are the most requested in the city? (understand where is a business necessity)
2. What is the average/maximum price a user would pay for reserving a parking spot? (understand what is the optimal range of prices and if could be dinamic)

[Back to top](/sprint-2/Sprint%202.md#sprint-2)

## 2.  Implemented functionalities.
1. **Real-Time Location with GPS**: This functionality utilizes the phone's GPS sensor to provide real-time location tracking. It allows users to see their current location on a map within the app, making it easier to find nearby parking spots or navigate to their destination.

2. **Answering Type 2 Questions**: As mentioned earlier, this functionality addresses Type 2 questions related to parking reservations, history, and recommendations. It provides answers to questions such as reservation duration, reservation history, and recommends nearby parking spots based on user preferences.

3. **Context-Aware Dark Mode**: This functionality adapts the app's appearance based on the time of day or ambient light conditions. For example, it switches to a dark mode at night or when the device's brightness is lowered, providing a more comfortable viewing experience in low-light situations.

4. **Smart Feature - Personalized Recommendations**: This feature employs smart algorithms to analyze user behavior and preferences. It can recommend parking spots based on historical usage patterns, suggesting the most frequently used parking locations or notifying the user when a preferred spot becomes available.

5. **User Authentication**: User authentication is essential for security and personalization. Users can create accounts, log in, and access personalized features such as saving favorite parking locations and viewing reservation history. This authentication is connected to the backend for data security.

6. **External Service Integration - Firebase User Registration**: This functionality integrates with an external service, specifically Firebase, for user registration. When users create accounts or log in, their authentication and registration data are securely managed on Firebase servers, ensuring data consistency and security across devices and platforms.
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
We are using the Model–View–ViewModel (MVVM) architecture to achieve a separation of concerns, improve code maintainability, and enhance the user interface experience. Additionally, Firebase enables automatic load balancing and efficient data management, contributing to the scalability and reliability of our system. In the second diagram, we have defined the views that the app will use to provide services and depict user interactions. Hence, we are using Google Analytics for Firebase to answer critical business questions and enhance our system. Finally, we leverage cloud storage and a NoSQL database to streamline data storage, taking advantage of the flexibility and scalability that NoSQL databases offer. We also utilize HTTPS for secure payment processing.








[Back to top](/sprint-2/Sprint%202.md#sprint-2)

## 6. Implementation of architectural design.
**will be evaluate in the viva vocce**

[Back to top](/sprint-2/Sprint%202.md#sprint-2)

## 7. Implementation of business questions.

**will beevaluated in the viva vocce**

[Back to top](/sprint-2/Sprint%202.md#sprint-2)


## 8. views

### Kotlin views: These views were displayed in the repositroy called Android_Kotlin located in this Organization
### 8.1.1 Main page
![image](https://github.com/ISIS3510-202320-Team13/Wiki/assets/89409633/73e11f44-3e8c-426a-82c4-99fc5b9a8a75)

### 8.1.2 Sign up page
![image](https://github.com/ISIS3510-202320-Team13/Wiki/assets/89409633/0f25a0bc-cf5b-4f3e-ad39-9f22935b8e19)




### 8.1.3 Parking Lot Detail page
![image](https://github.com/ISIS3510-202320-Team13/Wiki/assets/57652524/34c9006b-5e67-4aba-beae-18578abdde3d)

### 8.1.4. Booking details
![image](https://github.com/ISIS3510-202320-Team13/Wiki/assets/57652524/ff6fd48f-af04-4914-b83c-fb21220144ac)


### 8.1.5 map view

![image](https://github.com/ISIS3510-202320-Team13/Wiki/assets/89409633/b99f0db2-b45d-450f-8215-5dbddaacda14)

![image](https://github.com/ISIS3510-202320-Team13/Wiki/assets/89409633/7c141c96-b103-454a-80ac-e61219a40b99)

### 8.1.6 login view 

![image](https://github.com/ISIS3510-202320-Team13/Wiki/assets/89409633/fc696ebd-584f-48de-8f59-f109292cc993)

![image](https://github.com/ISIS3510-202320-Team13/Wiki/assets/89409633/178aac97-06f0-436a-b9e4-a7032c9656ea)


https://github.com/ISIS3510-202320-Team13/Wiki/assets/89409633/1c2e7323-9c88-4aa4-abcd-4c0579b4efd2


### Flutter views: These views were displayed in the repositroy called Flutter located in this Organization
### 8.2.1 Home page
<img src='https://github.com/ISIS3510-202320-Team13/Wiki/blob/main/assets/MS7/home_page_flutter.jpg' width='300'>

### 8.2.1 Near Parkings page
<img src='https://github.com/ISIS3510-202320-Team13/Wiki/blob/main/assets/MS7/near_parkings_flutter.jpg' width='300'>

### 8.3.1 Payment view
<img src='https://github.com/ISIS3510-202320-Team13/Wiki/assets/69475004/b6e79a2c-c01b-441b-b7bc-540b07c3bb81' width='300'>

### 8.3.2 Checkout View
<img src='https://github.com/ISIS3510-202320-Team13/Wiki/assets/69475004/5e6b135d-0ad3-44bb-9dff-229991c006ce' width='300'>


### 8.2.* Short funcioning video


https://github.com/ISIS3510-202320-Team13/Wiki/assets/60227071/1b5e8fd1-4cfc-4890-b993-077050f14c00



https://github.com/ISIS3510-202320-Team13/Wiki/assets/69475004/90ad3ede-2d85-4c93-86ef-175f5915f22f

## 9. Video Ethics

[Back to top](/sprint-2/Sprint%202.md#sprint-2)


