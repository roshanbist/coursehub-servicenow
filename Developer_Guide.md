# Course Hub

Welcome to the **Course Subscription Application**! This boilerplate application is designed to help you get started with building a simple course subscription application on the ServiceNow platform. It provides the foundational data model and basic configurations, allowing you to focus on implementing the required features and enhancing the application.

## Table of Contents

- [Introduction](#markdown-header-introduction)
- [Prerequisites](#markdown-header-prerequisites)
- [Getting Started](#markdown-header-getting-started)
- [Application Overview](#markdown-header-application-overview)
- [Navigating the Application](#markdown-header-navigating-the-application)
- [Next Steps](#markdown-header-next-steps)
- [Additional Resources](#markdown-header-additional-resources)
- [Support](#markdown-header-support)

## Introduction

The Course Subscription Application allows learners to view available courses and subscribe to them. This boilerplate provides the essential components to help you implement features such as fetching course lists, subscribing to courses, and displaying subscribed courses.

> The goal is to have workable simple version of application that involves ServiceNow in some way. We do not expect you to understand whole ServiceNow platform in couple of days. 

## Prerequisites

Before you begin, ensure you have the following:

- **ServiceNow Personal Developer Instance (PDI)**
    - Sign up at [developer.servicenow.com](https://developer.servicenow.com/) if you don't have one.
- **ServiceNow Studio Access**
    - You will use Studio to import and manage the application.
- **Git and Remote Repository**
    - The repository is public; you should be able to clone it to your local machine and push it to the desired remote repository of your choice.

## Getting Started

Follow these steps to set up the application in your ServiceNow instance.

### 1. Set Up Your ServiceNow Developer Instance

 **Sign Up for a PDI**

- Visit [developer.servicenow.com](https://developer.servicenow.com/) and create an account.
- Request a Personal Developer Instance (PDI) and follow the instructions to activate it.

 **Access Your PDI**

- Once your instance is ready, log in using the credentials provided.

### 2. Clone the Application

 **Obtain the Repository URL**

- Get the HTTPS URL of this repository hosting the application.
- Clone it to your local machine.
- Create a remote repository on your desired provider (e.g., GitHub, GitLab).
- Change the remote to point to your new repository, then push the code to it.

 **Create Git Credentials in ServiceNow**

- In your PDI, navigate to **Connections & Credentials > Credentials**.
- Click **New** and select **Credential**.
- Select **Basic Auth Credentials**.
- Fill in the following:

    - **Name**: *Git Source Control Credential*
    - **Username**: *Your username*
    - **Password**: *Your app password or account password*
- Save the credential.

**Import the Application via Studio**
- Use the application navigator to go to **All > Studio**. DO NOT USE "ServiceNow Studio", use System Application > Studio
- You can now import the application that you pushed to your remote repository. Follow the guide: [Import App into the PDI](https://developer.servicenow.com/dev.do#!/learn/learning-plans/quebec/new_to_servicenow/app_store_learnv2_devenvironment_quebec_importing_an_application_from_source_control).

**Verify the Import**
- Once the import is complete, you should see the application files in Studio.
- Ensure there are no errors or conflicts.

## Application Overview

### Data Model

The application consists of three main tables:

1. **Course** (`x_quo_coursehub_course`)
2. **Learner** (`x_quo_coursehub_learner`)
3. **Course Subscription** (`x_quo_coursehub_course_subscription`)

### Tables and Fields

All the tables come with default fields: `sys_id`, `created`, `created_by`, `updated`, `updated_by`.

#### Course Table

- **Label**: Course
- **Name**: `x_quo_coursehub_course`

**Fields**:

- **Title** (`title`): String (Max Length: 100, Mandatory)
- **Description** (`description`): String (Max Length: 500)
- **Type** (`type`): Choice (Options: Online, Offline, Hybrid)
- **Duration** (`duration`): Duration (Days Hours:Minutes:Seconds)

#### Learner Table

- **Label**: Learner
- **Name**: `x_quo_coursehub_learner`

**Fields**:

- **User Account** (`user_account`): Reference to `sys_user` (Mandatory)
- **Admission Date** (`admission_date`): Date/Time

#### Course Subscription Table

- **Label**: Course Subscription
- **Name**: `x_quo_coursehub_course_subscription`

**Fields**:

- **Learner** (`learner`): Reference to `x_quo_coursehub_learner` (Mandatory)
- **Course** (`course`): Reference to `x_quo_coursehub_course` (Mandatory)
- **Subscription Date** (`subscription_date`): Date/Time (Defaults to current date/time)

### Access Permission

The following table outlines the access permissions for the roles **x_quo_coursehub.manager** and **x_quo_coursehub.user** across the application's tables.


| **Table**                                           | **Permission** | **x_quo_coursehub.manager** | **x_quo_coursehub.user** |
|-----------------------------------------------------|----------------|------------------------------|--------------------------|
| **Course**<br>`x_quo_coursehub_course`              | **Create**     | Yes                          | No                       |
|                                                     | **Read**       | Yes                          | Yes                      |
|                                                     | **Update**     | Yes                          | No                       |
|                                                     | **Delete**     | Yes                          | No                       |
| **Learner**<br>`x_quo_coursehub_learner`            | **Create**     | Yes                          | Yes                      |
|                                                     | **Read**       | Yes                          | Yes                      |
|                                                     | **Update**     | Yes                          | Yes                      |
|                                                     | **Delete**     | Yes                          | No                       |
| **Course Subscription**<br>`x_quo_coursehub_course_subscription` | **Create** | Yes | Yes |
|                                                     | **Read**       | Yes                          | Yes                      |
|                                                     | **Update**     | Yes                          | Yes                      |
|                                                     | **Delete**     | Yes                          | No                       |

## Navigating the Application

### Accessing the Application

**Open the Application Navigator**:

- In your ServiceNow instance, use the filter navigator on the left. Click the **"All"** menu item on the top navigation bar to open the Application Navigator.
- You should find the **"CourseHub"** application menu.
- **Courses** and **Learners** are listed under **"CourseHub"**.

**Explore the Tables, Lists, and Forms**

- Click on **"Course"** or **"Learners"**.
- Create a few relevant records using the standard UI.


## CourseHub Experience

Now that you have the application set up, you can start implementing the required features. You should use servicenow [UI Builder (UIB)](https://www.servicenow.com/docs/csh?topicname=ui-builder-overview.html&version=latest) to build simple interface that works.

> Follow the assignment instructions provided, focus on implementing features that you can.

### Build UI Experience

1. Using servicenow top navigation bar, Go to All > UI Builder
2. Find and select existing Experience: Qdx Course Hub or Create new
3. Start building using "Home" page or some other pages as per your design
4. Modify and design the course hub as you wish using the building blocks available.

> **Tips**: start by adding the Layout first, then build using the Components.

### Key Ingredients

The servicenow UI Builder (UIB) is WYSIWYG "low code" tool, it designed to deliver UI experiences for speed and scale. The "pro code" user can built their own custom component using Next Experience UI Framework, but that is out-of-scope. Focus on following:

#### Next Experience Components

Navigate to readily available [components portal](https://developer.servicenow.com/dev.do#!/reference/next-experience/components), on the side bar make sure to filter with "Yokohama" release and "Available in UIB". Explore the relevant component definition and find the configuration details for how to use within UI Builder.

#### Data Binding

The data binding is crucial for the components to be dynamic, the [data binding modal](https://www.servicenow.com/docs/csh?topicname=connect-data-components.html&version=latest) make it easy. You can find the information.

#### Data Resources

These building blocks are available under the "Data and Scripts", these are used to provide dynamic data to the components, find more information [here](https://www.servicenow.com/docs/csh?topicname=data-resources.html&version=latest). The data resources are sometime referred as Data Broker, one can create custom Data Broker for REST API, GraphQL, data Transform, and custom server-side script. We recommend to focus on data resources that is readily available:

* Create Record
* Look up a single record
* Look up multiple records
* Update Record
* Delete Record
* Delete Multiple Records

#### Client State Parameters

One way to think about UIB Client state parameters is state management solutions available for reactive JavaScript UI libraries available out there in wild, you can find more information from [here](https://www.servicenow.com/docs/csh?topicname=client-state-parameters.html&version=latest)

#### Client Scripts

It provides the scripting capabilities in UIB to customize interaction using JavaScript that connects client state through events, find the more information here (https://developer.servicenow.com/dev.do#!/learn/courses/yokohama/app_store_learnv2_uibuilder_yokohama_ui_builder/app_store_learnv2_uibuilder_yokohama_client_side_interactions_in_ui_builder/UCS_WhatAreClientScripts_yokohama).

### UIB API Reference

* [Api - UIB](https://www.servicenow.com/docs/csh?topicname=apiAPI.html&version=latest)
* [Helpers - UIB](https://www.servicenow.com/docs/csh?topicname=helpersAPI.html&version=latest)

### Need Comprehensive Course

If you need a learning course on UI Builder, and want to invest your time. The servicenow [developer portal](https://developer.servicenow.com) have you covered. UIB [learning course](https://developer.servicenow.com/dev.do#!/learn/courses/yokohama/app_store_learnv2_uibuilder_yokohama_ui_builder) covers following topics:

* Pages in UIB
* Events in UIB
* Client-side Interactions in UIB
* Data Resources in UIB
* Modals in UIB

## Additional Resources

- **ServiceNow Developer Site**: [developer.servicenow.com](https://developer.servicenow.com/)
- **ServiceNow Documentation**:
    - [Building Applications on the Now Platform](https://docs.servicenow.com/bundle/quebec-application-development/page/build/applications/concept/build-applications.html)
    - [Tables and Data Management](https://docs.servicenow.com/bundle/quebec-platform-administration/page/administer/table-administration/concept/c_TableAdministration.html)
    - [Pro-Code Development](https://docs.servicenow.com/bundle/quebec-application-development/page/build/applications/concept/building-pro-code-applications.html)
    - [REST API Reference](https://developer.servicenow.com/dev.do#!/reference/api/quebec/rest)
    - [UIB: Component config and repeater](https://www.servicenow.com/docs/csh?topicname=configure-comp-and-repeaters.html&version=latest)
    - [UIB: Glossary](https://www.servicenow.com/docs/csh?topicname=ui-builder-glossary.html&version=latest)
    - [UIB: Config data resource](https://www.servicenow.com/docs/csh?topicname=add-data-resources.html&version=latest)
    - [Import Application from Git rep](https://docs.servicenow.com/csh?topicname=t_ImportAppFromSourceControl.html&version=latest)


## Push Changes

To commit and push your changes:

1. Navigate to System Application > Studio in the application navigator
2. Once in Studio, click on the Source Control menu in the top nav bar
3. Select Commit Changes from the dropdown menu
4. Enter a meaningful commit message describing your changes
5. Select the artifact changes, and follow the steps in modal window.

---

We hope this boilerplate helps you get started quickly. Good luck with your assignment, and we look forward to discussing your work in the interview!

---
