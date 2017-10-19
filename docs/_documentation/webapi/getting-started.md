---
layout: documentation
category: WebAPI
title: Getting Started
order: 1
---

First of all, please read this to understand [SOAP vs REST](http://spf13.com/post/soap-vs-rest/)

## Introduction

When following the guideline of this document the resulting API(Application Programming Interface) will reach Level 1 of the [Richardson Maturity Model](https://www.martinfowler.com/articles/richardsonMaturityModel.html) ([1], [4]). That means a resource model has been provided, use of proper HTTP(S) methods has been made, use of appropriate HTTP headers have been identified, and HTTP status codes are used in responses.

The top level - Level 3 - of the Richardson Maturity Model will not be reached. This third level assumes to make use of hypermedia controls: such controls allow REST (Representational State Transfer)servers to inform REST clients about the APIs that may be invoked in the current state of the application. While this is promising in terms of, for example, maintainability (e.g. APIs may be changed without clients having to understand these changes), no best practices have been established yet to deal with this.

## Overall Approach

The following major steps should be followed to create a RESTful (Level 2) API (see Figure 1).

<img width="1140" src="https://github.com/gmfjlr/DevForDev/raw/master/docs/assets/img/webapi/webapi%20-%20image1.png">

**Figure 1: REST API Design Approach**

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

**Figure 2: Sample Data Model**

Figure 2 depicts a sample data model that will be used in the following sections to give examples on how to apply the given guidelines.

The data model is an important source to determine an appropriate resource model. However, the way clients interact with the API is a significant influencer of the resource model derived from the data model ("clients win over data"). The domain model drives the implementation of the API, while the resource model is driven by client interactions. But typically, the resource model will "follow the data model".

## Resource Model

The resource model specifies the resources that are processed by the API. Several kinds of resources will derived from both, the data model as well as the corresponding processing requirements.

### Atomic Resources

The most basic decision to be made for deriving resources is identifying entities of the data model that are exchanged as a whole via the API. Such entities become atomic resources.

For example, based on the sample data model in Figure 2, the Customer entity will become such an atomic entity. This is because details about a customer like his address, payment information etc. will be accessed in several scenarios suported by the API.

### Collection Resources

The next decision to be made is whether atomic resources of the same type are needed to be grouped into a set. Such bundles become collection resources.

For example, products will become a collection resource because the application supports a catalogue that allows browsing through (subsets of) all products available. Note, that there is no products entity type in the data model. Because the application requires such a collection resource we derive it from the data model and give it a new name that corresponds to the plural of the name of the grouped entity type.

As another example, items will become a collection resource that represent all items contained in a shopping cart of a certain customer. This collection will be scoped, i.e. only the items in a specific shopping cart are of interest but not the set of all items in all shopping carts (see section 5.6 for more details on scoping).

Finally, whenever the API supports the creation of an instance of one of the entity types of the data model, this entity type results in a corresponding collection resource. For example, a new customer may register with the application resulting in a new instance of the Customer entity type. Thus, Customers will become a collection resource.

### Composite Resources

Sometimes, instances of groups of different entity types are manipulated as a whole because these instances are perceived as aggregates, e.g. they are typically collectively retrieved or deleted. Such groups become composite resources.

For example, a Shopping Cart is a composite resource because it is often retrieved or deleted as a whole, i.e. with all of its encompassed items.



### Controller Resource

Controller resources are used when multiple resources have to be manipulated in a single API call in order to maintain data consistency. If integrity rules between resources must be obeyed, a client would have to understand these rules like the order in which resources are to be manipulated. By providing a controller resource to manipulate these resource in a single API call relieves the client from having to understand these rules - a significant contribution to loose coupling.

For example, deleting each individual item of a shopping cart one after the other may result in consistency problems in case an error occurs after having deleted only the first few items while others are still left in the shopping cart: a customer requesting the shopping cart just at this point in time of failure will realize a "broken" shopping cart.

Another example is the update of two account resources to realize a funds transfer - the classical motivation for ACID (Atomicity, Consistency, Isolation and Durability) transactions. Each of these two accounts is an atomic resource, i.e. controller resources are different from composite resources.

### Processing Function Resources

Processing function resources (aka computing resources) provide access to functions that either process particular resources, or that perform certain resource independent computations. In practice, processing function resources are often used for predefined partial updates of a resource.

For example, changing the status of a resource like the price of a product, or getting the official exchange rate between two currencies can be realized by means of a processing function resource.

**Note**: Partial updates are addressed by the HTTP PATCH method [7]. The problem with PATCH is two-fold:

  - The PATCH method is not (yet) supported by all web servers. Of course, this problem may go away.
  - The syntax and semantics for each use of the PATH method must be crisply defined: The resource enclosed in the body of a PATCH method is an instruction document, i.e. a set of instructions precisely describing what has to be updated and how, and all of these instructions must be performed atomically. Especially, the media type of this instruction document is typically different from the media type of the resource that is to be modified by the PATCH. The instruction document may be perceived as a sort of transaction on the resource to be manipulated.

This results in broad exploitation of processing function resources for realizing partial updates.

### Interpreting Relationships

One of the basic problems of deriving a resource model from a data model is in interpreting the relationships between entity types of the data model.

If manipulating instances of a certain entity type does not require the traversal of its associated relationships, then such an entity type is a candidate for an atomic resource: if the instances have to be available via the API, the entity type is transformed into an atomic resource in a one-one correspondence.

Collection resources may be subject to an interpretation of its associated relationship types, i.e. collections may only make sense as children of other resources (so-called scoped collections).

For example: The Products collection resource is not scoped, i.e. this collection is a first class resource of the sample resource model. In contrast to this, the Items collection resource in fact is scoped: the collection of all items in all shopping carts is typically not of interest at all, but all items within a certain shopping cart is of interest. Thus, collections of Items dependent on a certain shopping cart is a collection resource.

If the API has to support the direct creation of instances of an entity type, this entity type results in a collection resource. This is because in the REST paradigm a collection resource is a factory for its members. The entity type itself is the basis for atomic resources that are the members of the collection resource.

Processing function resources as well as controller resources result from functional requirements: they are typically not immediately derived from the data model but from update requirements or from requirements to derive information that may not even be related to some other resources.





