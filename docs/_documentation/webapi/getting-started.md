---
layout: documentation
category: WebAPI
title: Getting Started
order: 1
---

## Introduction

When following the guideline of this document the resulting API(Application Programming Interface) will reach Level 1 of the Richardson Maturity Model ([1], [4]). That means a resource model has been provided, use of proper HTTP(S) methods has been made, use of appropriate HTTP headers have been identified, and HTTP status codes are used in responses.

The top level - Level 3 - of the Richardson Maturity Model will not be reached. This third level assumes to make use of hypermedia controls: such controls allow REST (Representational State Transfer)servers to inform REST clients about the APIs that may be invoked in the current state of the application. While this is promising in terms of, for example, maintainability (e.g. APIs may be changed without clients having to understand these changes), no best practices have been established yet to deal with this.

## Overall Approach

The following major steps should be followed to create a RESTful (Level 2) API (see Figure 1).

<img width="1140" src="https://github.com/gmfjlr/DevForDev/raw/master/docs/assets/img/webapi/webapi%20-%20image1.png"> 

First, a model of the data to be manipulated by the API is created. From this data model the resources of the API will be determined; typically, here is no one-to-one correspondence between data model elements and resources of the API, especially because new kinds of resources will typically be derived. For each of the resources the representations supported by the APIs have to be determined. Next, these resources must be named properly by means of URIs (Uniform Resource Identifiers). For each of the resources the HTTP methods used to perform the required application functions have to be decided; this includes the use of applicable HTTP headers. Special behavior required by the application (e.g. concurrency control, long running requests) has to be decided. Finally, potential error situations have to be identified and corresponding error messages have to be designed.

**Note**: Although Figure 1 sketches the approach as a sequential process, following it stepby-step is not always needed. For example
  
  - The data model may already be known. In this case, the first step will be omitted.
  - The resource model has already been decided. In this case, the second step may be left out. But in case the data model is not precisely specified, it may be worth to perform step 1.
  - Your API is very straight-forward, e.g. you don't expect concurrent updates of your resources, or none of your APIs kick-off long-running actions. Then you will leave out the step to "determine special behavior".

Each individual step of the overall approach will be detailed in the next sections.

## Data Model

The data model behind an API can be specified by any conceptual data modeling language like the entity-relationship Model or UML Class Diagrams. In what follows we assume the use of the entity-Relationship Model.

The main purpose of the data model behind an API is to specify the properties of the resources manipulated by an API in an abstract (i.e. implementation independent) manner. By specifying the attributes of the entity types of the data model no early decision is made about the format and media type in which instances of the entity types (aka representations in REST) are exchanged - this decision will be made later, and it can be changed during the lifetime of an API. Thus, it results in more flexibility in the development process.

<img width="1140" src="https://github.com/gmfjlr/DevForDev/raw/master/docs/assets/img/webapi/webapi%20-%20image2.png"> 

Figure 2 depicts a sample data model that will be used in the following sections to give examples on how to apply the given guidelines.

The data model is an important source to determine an appropriate resource model. However, the way clients interact with the API is a significant influencer of the resource model derived from the data model ("clients win over data"). The domain model drives the implementation of the API, while the resource model is driven by client interactions. But typically, the resource model will "follow the data model".
