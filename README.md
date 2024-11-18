This repository contains only the documentation about [DashboardProject](https://github.com/immanaro2497/DashboardProject). The original might be private.

# Contents
* [About App](#about-app)
* [App Videos](#app-videos)
* [Technologies](#technologies)
* [App Architecture](#app-architecture)
* [TDD and Clean Architecture](#tdd-and-clean-architecture)
* [App Features and Functionalities](#app-features-and-functionalities)
* [Time for adding new similar feature](#time-for-adding-new-similar-feature)
* [Use Cases](#use-cases)

## About App
An app which fetches data from server and displays to user. The app stores data in offline database, so user can access data when there is no network connection.

## App Videos

https://github.com/user-attachments/assets/9292d65d-d57b-40a0-89d6-883310e49c49

## Technologies

|                      |                             |
|----------------------|-----------------------------|
| IDE                  | Xcode 16                    |
| Programming Language | Swift 5(Swift concurrency)  |
| UI                   | SwiftUI(Light/Dark mode)    |
| Networking           | URLSession                  |
| Offline database     | Realm                       |
| Remote configuration | Firebase remote config      |
| Testing              | TDD, XCTest                 |
| Version control      | Git, Github                 |
| Architecture         | MVVM, Clean architecture    |
| Platform support     | iOS 16, iPadOS 16           |
| Language             | English, Arabic             |

## App Architecture
This whole project is divided into 3 projects. By separating into projects, the changes can be done independently and improve build times.

### Dashboard Feed Project
1. Dashboard Feed Target - Contains API, Persistence, Presentation layers and 3rd Party framework
2. Dashboard Feed Tests Target - Contains tests for Dashboard Feed Target
3. Dashboard Feed API End to End Tests Target - Contains test for API integration.

### Dashboard Log Project
1. Dashboard Log Target - Contains Remote Config and 3rd Party framework

### Dashboard App Project
1. Dashboard App Target - Contains Main App and App UI. Depends on Dashboard Feed Project and Dashboard Log Project.

<img width="253" alt="ProjectStructure" src="https://github.com/user-attachments/assets/e06389ef-07b0-4c4f-a867-b72742210517">

## TDD and Clean Architecture
Developed API, Persistence and Presentation layers using Test Driven Development and Clean architecture for better code quality, testability, maintainability and reusability.   

Test coverage in Dashboard Feed Project is 99.5%   

<img width="600" alt="TestCoverage" src="https://github.com/user-attachments/assets/5904e00a-3d7a-4b70-9196-0284eeafab7b">   

<img width="600" alt="SeparationOfLayers" src="https://github.com/user-attachments/assets/66e98839-517c-4f15-a82c-094f15550dfe">

## App Features and Functionalities

### Sync(Downloading data)
App downloads data from server on user pull down to refresh action.   
In Dashboard screen app downloads both job and invoice data.

In individual list screen app will download only the related data. This design will benefit the user by using less data and quicker download as the download contains only the current screen related data.

### Custom Card view
After applying some logic to the data downloaded it will be displayed to the user in card view.   
In invoice card view the amount is converted to dollar format in app.

### Custom chart view
The custom chart view displays the data in descending order.

### Custom chart legend view
This view is created based on custom calculation.   
The legend view displays the types of data available in the chart.   
The text views inside has a justification alignment and adapts to orientation changes. 

Portrait|Landscape
--|--
<img height="400" alt="ChartLegendViewPortrait" src="https://github.com/user-attachments/assets/48e5c25d-d69c-4715-9739-7174eba49a24">|<img width="400" alt="ChartLegendViewLandscape" src="https://github.com/user-attachments/assets/ee2a6d3d-9044-4b35-9282-08ccf0afe6f1">

### Navigation flow
On selecting the card view, the user will be navigated to new screen which displays the list data, which is grouped into tabs based on their type.

By default the user will be navigated to the first tab.   
On selecting a type in chart legend view, this will navigate to the exact tab. This design was for improving user experience.

### Custom Navigation title
The Navigation title is a custom view.
The back button will be displayed based on number of screens pushed in the stack.

### Individual list screen
Reused the chart view from the main screen.   
Custom horizontal scrollable tabs with smooth animations for better user experience.   
The list rows are custom views designed for row.

### Job list row date calculation
A custom calculation for showing start and end date.

1. Current day start and end time   
Data - '2024-11-15T11:45:37.320Z', '2024-11-15T18:45:37.320Z'   
Display - 'Today, 11:45 - 18:45'

2. Same day start and end time   
Data - '2024-11-16T11:45:37.320Z', '2024-11-16T18:45:37.320Z'   
Display - '16/11/2024, 11:45 - 18:45'

3. Different day start and end time   
Data - '2024-11-16T11:45:37.320Z', '2024-11-17T18:45:37.320Z'   
Display - '16/11/2024, 11:45 AM → 17/11/2024, 18:45 PM'

### Alert for error
When download fails an alert will be shown to user.

<img height="400" alt="ErrorAlert" src="https://github.com/user-attachments/assets/ce25568a-fbaf-4e00-94e3-042e6d1052fb">

### Custom toast view for status updates
A toast view for showing some status updates to user.   
When appear the toast view will blink to grab user attention. And auto hides after 1 second.   
Whenever sync completes successfully toast view will be displayed.

### Light/Dark mode
Supports light and dark mode.   

<img height="400" alt="Darkmodelist" src="https://github.com/user-attachments/assets/341c05ec-d8ff-4572-9189-10ce893f60f0">

### Localization
Supports English(Left To Right), Arabic(Right To Left).   
English is the main language.   
Static texts in app were converted to arabic and added to string catalog.

Main screen|List screen
--|--
<img height="400" alt="MainScreenArabic" src="https://github.com/user-attachments/assets/35bdc82c-dab1-4a4d-8fa6-611006543246">|<img height="400" alt="ListScreenArabic" src="https://github.com/user-attachments/assets/7cbe2399-82b7-4775-9fc6-e6b0b98a50b1">

### Enabling/Disabling feature
Using firebase remote config, a feature can be enabled and disabled based on needs.

Firebase remote config|App job disabled from remote config
--|--
<img width="500" alt="Firebase remote config" src="https://github.com/user-attachments/assets/c24cd4f9-b457-4906-9489-b06d5382f003">|<img height="400" alt="JobDisabled" src="https://github.com/user-attachments/assets/5a277fbb-547a-4b74-905f-df300c7bbddd">

## Time for adding new similar feature
First worked on job feature, took me a week to complete API(including test), Persistence(including test), Presentation(including test), Card UI, List UI, Light/Dark mode support.

Then started working on invoice feature, since the funtionality is similar, i was able to reuse all the layers from job feature. And completed invoice feature in half day with tests.

## Use Cases

### Load Job Data From Remote Use Case
 
#### Data:
- URL

#### Primary course (happy path):
1. Execute "Load Job Data" command with above data.
2. System downloads data from the URL.
3. System creates job details from valid data.
4. System delivers job details.

#### Invalid data – error course (sad path):
1. System delivers invalid data error.

#### No connectivity – error course (sad path):
1. System delivers connectivity error.

---

### Load Invoice Data From Remote Use Case

#### Data:
- URL

#### Primary course (happy path):
1. Execute "Load Invoice Data" command with above data.
2. System downloads data from the URL.
3. System creates invoice details from valid data.
4. System delivers invoice details.

#### Invalid data – error course (sad path):
1. System delivers invalid data error.

#### No connectivity – error course (sad path):
1. System delivers connectivity error.

---

### Load Job Data From Local Use Case

#### Primary course (happy path):
1. Execute "Load Job Data" command.
2. System retrieves job data from local.
3. System creates job details from local data.
4. System delivers job details.

#### Retrieval error course (sad path):
1. System delivers error.

---

### Load Invoice Data From Local Use Case

#### Primary course (happy path):
1. Execute "Load Invoice Data" command.
2. System retrieves invoice data from local.
3. System creates invoice details from local data.
4. System delivers invoice details.

#### Retrieval error course (sad path):
1. System delivers error.

---

### Save Job Data Use Case

#### Data:
- Job Data

#### Primary course (happy path):
1. Execute "Save Job Data" command with above data.
2. System deletes old data.
3. System saves new data.
4. System delivers success message.

#### Deleting error course (sad path):
1. System delivers error.

#### Saving error course (sad path):
1. System delivers error.

---

### Save Invoice Data Use Case

#### Data:
- Invoice Data

#### Primary course (happy path):
1. Execute "Save Invoice Data" command with above data.
2. System deletes old data.
3. System saves new data.
4. System delivers success message.

#### Deleting error course (sad path):
1. System delivers error.

#### Saving error course (sad path):
1. System delivers error.

---

## Model Specs

### Job Data

| Property      | Type                    |
|---------------|-------------------------|
| `id`          | `UUID`                  |
| `jobNumber`   | `Int`                   |
| `title`       | `String`                |
| `startTime`   | `Date` (ISO8601 String) |
| `endTime`     | `Date` (ISO8601 String) |
| `status`      | `String`                |

### Payload contract

```
GET /jobs

200 RESPONSE

[
    {
        "id": "a UUID",
        "jobNumber": 1,
        "title": "a title",
        "startTime": "2024-11-15T13:18:51.102Z",
        "endTime": "2024-12-11T13:18:51.102Z",
        "status": "a status"
    },
    {
        "id": "another UUID",
        "jobNumber": 2,
        "title": "another title",
        "startTime": "2024-11-16T13:18:51.102Z",
        "endTime": "2024-12-13T13:18:51.102Z",
        "status": "another status"
    }
    ...
]

```

### Invoice Data

| Property         | Type          |
|------------------|---------------|
| `id`             | `UUID`        |
| `invoiceNumber`  | `Int`         |
| `customerName`   | `String`      |
| `total`          | `Int`         |
| `status`         | `String`      |

### Payload contract

```
GET /invoices

200 RESPONSE

[
    {
        "id": "a UUID",
        "invoiceNumber": 1,
        "customerName": "a name",
        "total": 100,
        "status": "a status"
    },
    {
        "id": "another UUID",
        "invoiceNumber": 2,
        "customerName": "another name",
        "total": 200,
        "status": "another status"
    }
    ...
]

```
