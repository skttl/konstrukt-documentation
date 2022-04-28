---
description: Configuring encrypted properties in Konstrukt, the back office UI builder for Umbraco.
---

# Encrypted Properties

{% hint style="info" %}
**Work in Progress:** The documentation for this page is currently in progress.
{% endhint %}

## Defining encrypted properties

#### **AddEncryptedProperty(Lambda encryptedPropertyExpression) : KonstruktCollectionConfigBuilder&lt;TEntityType&gt;**

Adds the given property to the encrypted properties collection. Property must be of type `String`. When set, the property will be encrypted/decrypted on write/read respectively.

````csharp
// Example
collectionConfig.AddEncryptedProperty(p => p.Email);
````