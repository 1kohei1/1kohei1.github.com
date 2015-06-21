---
layout: post
title: "Hello World"
description: ""
category: 
tags: ["sample"]
---
{% include JB/setup %}
In addition to the messaging behavior covered in the previous chapter, an object also encapsulates data through its properties.

This chapter describes the Objective-C syntax used to declare properties for an object and explains how those properties are implemented by default through synthesis of accessor methods and instance variables. If a property is backed by an instance variable, that variable must be set correctly in any initialization methods.

If an object needs to maintain a link to another object through a property, it’s important to consider the nature of the relationship between the two objects. Although memory management for Objective-C objects is mostly handled for you through Automatic Reference Counting (ARC), it’s important to know how to avoid problems like strong reference cycles, which lead to memory leaks. This chapter explains the lifecycle of an object, and describes how to think in terms of managing your graph of objects through relationships.

## Properties Encapsulate an Object’s Values

Most objects need to keep track of information in order to perform their tasks. Some objects are designed to model one or more values, such as a Cocoa NSNumber class to hold a numeric value or a custom XYZPerson class to model a person with a first and last name. Some objects are more general in scope, perhaps handling the interaction between a user interface and the information it displays, but even these objects need to keep track of user interface elements or the related model objects.

	@interface XYZPerson : NSObject
	@property NSString *firstName;
	@property NSString *lastName;
	@end

In this example, the `XYZPerson` class declares string properties to hold a person’s first and last name.

Given that one of the primary principles in object-oriented programming is that an object should hide its internal workings behind its public interface, it’s important to access an object’s properties using behavior exposed by the object rather than trying to gain access to the internal values directly.

## Use Accessor Methods to Get or Set Property Values

You access or set an object’s properties via accessor methods:
 	NSString *firstName = [somePerson firstName];
 	[somePerson setFirstName:@"Johnny"];

By default, these accessor methods are synthesized automatically for you by the compiler, so you don’t need to do anything other than declare the property using `@property` in the class interface.

