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

The
following major steps should be followed to create a RESTful (Level 2) API (see
Figure 1).

