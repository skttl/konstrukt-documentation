---
description: Configuring sections in Konstrukt, the back office UI builder for Umbraco.
---

# Sections

A section is a distinct area of the Umbraco backoffice, such as content, media, etc, and is accessed via a link in the main menu at the top of the Umbraco interface. Konstrukt allows you to define multiple sections in order to organise the management of your models into logical sections.

## Defining a section

You define a section by calling one of the `AddSection` methods on the root level `KonstruktConfigBuilder` instance.

#### **AddSection(string name, Lambda sectionConfig = null) : KonstruktSectionConfigBuilder**

Adds a section to the Umbraco menu with the given name.

```csharp
// Example
config.AddSection("Repositories", sectionConfig => {
    ...
});
```

#### **AddSectionBefore(string beforeAlias, string name, Lambda sectionConfig = null) : KonstruktSectionConfigBuilder**

Adds a section to the Umbraco menu with the given name before the section with the given alias.

```csharp
// Example
config.AddSectionBefore("settings", "Repositories", sectionConfig => {
    ...
});
```

#### **AddSectionAfter(string afterAlias, string name, Lambda sectionConfig = null) : KonstruktSectionConfigBuilder**

Adds a section to the Umbraco menu with the given name after the section with the given alias.

```csharp
// Example
config.AddSectionAfter("media", "Repositories", sectionConfig => {
    ...
});
```

## Changing a section alias

#### **SetAlias(string alias) : KonstruktSectionConfigBuilder**

Sets the alias of the section.

**Optional:** When adding a new section, an alias is automatically generated from the supplied name for you, however you can use the `SetAlias` method to override this should you need a specific alias.

```csharp
// Example
sectionConfig.SetAlias("repositories");
```

## Configuring the section tree

#### **Tree(Lambda treeConfig = null) : KonstruktTreeConfigBuilder**

Accesses the tree config of the current section. See [Trees documentation](trees.md) for more info.

````csharp
// Example
sectionConfig.Tree(treeConfig => {
    ...
});
````