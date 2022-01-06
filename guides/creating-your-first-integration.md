---
description: Creating your first integration with Konstrukt, the fluent administration panel builder for Umbraco.
---

# Creating your first integration

In this guide we'll take you through the steps needed for a basic implementation using Konstrukt to manage a single custom database table.

## Set up the database

Out of the box Konstrukt works using PetaPoco as the persistence layer as this is what ships with Umbraco. It is possible to use a custom [Repository](../api/repositories.md) if you prefer, but for the sake of getting started, we’ll assume you are using this default strategy.

Start by setting up a database table for your model (you might want to populate it with some dummy data as well whilst learning). We’ll use the following as an example:

```sql
CREATE TABLE [Person] (
    [Id] int IDENTITY (1,1) NOT NULL, 
    [Name] nvarchar(255) NOT NULL, 
    [JobTitle] nvarchar(255) NOT NULL, 
    [Email] nvarchar(255) NOT NULL, 
    [Telephone] nvarchar(255) NOT NULL, 
    [Age] int NOT NULL, 
    [Avatar] nvarchar(255) NOT NULL
);
```

## Configure your model

## Configure Konstrukt

## Access your UI

{% hint style="info" %}
**Good to know:** your product docs aren't just a reference of all your features! use them to encourage folks to perform certain actions and discover the value in your product.
{% endhint %}

## The basics

Projects are containers for task lists. Think of them as a library for everything your team needs to get done to complete or ship a project.

## Creating a project

Hit the big '+' button in your sidebar and select 'New Project' from the menu that pops up. Give your project a name, and you're good to go!
