---
description: Changelog for Konstrukt, the back office UI builder for Umbraco.
---

# Changelog

## v1.4.0
**Date:** 2022-07-12  
**Description:** Minor release with additional features and bug fixes

- Added [WithSection](../areas/sections.md#extending-an-existing-section) / [WithTree](../areas/trees.md#extending-an-existing-tree) API to create more logical API groupings and to set context for some APIs.
- Added [`AddTree`](../areas/trees.md#adding-a-tree-to-an-existing-section) support to allow adding a tree to an existing section (currently only able to add 1 Konstrukt tree per section).
- Added [Tree Group](../areas/trees.md#adding-a-group-to-a-tree) support to allow grouping root level tree folders / collections.
- Added [Tab Sidebar](../collections/editors.md#configuring-a-sidebar-to-a-tab) support to allow showing meta data on the right hand side of the editor.
- Added file upload support to the actions dialog
- Added a simple CSV Import action
- Added `HideLabel()` support to editor fields to explicitly hide the label.
- Added explicit Insert / Update methods to IKonstruktRepository and we now internaly use these instead of the Save method as the Save method isn't reliably able to determine if an entity is new or not.
- Added better support for transient / scoped repository dependencies (ie better support for EF Core DB contexts which are by default registered as scoped)
- Obsoleted root level APIs for `AddSection`, `AddDashboard` and `AddVirtualSubTree` which have now moved to sub configurations of the `WithSection` or `WithTree` APIs.
- Fixed bug with DataViews resolving the wrong filter when using groups and the data view has the same name as a view in a different group. We not prefix the data view alias with the group name to ensure uniqueness across groups.
- Fixed bug in child collections create dialog thinking it was always editing an existing entity and so wrongfuly trying to load an entity from the DB due to the fact the entity ID passed through to the dialog "0" when it should be "-1".

## v1.3.0
**Date:** 2022-07-06  
**Description:** Minor release with additional features and bug fixes

- Added [Virtual Sub Trees](../advanced/virtual-sub-trees.md) support
- Fixed save / delete notification events being passed the wrong model
- Fixed bug where connection strings with not provider cause an error

## v1.2.0
**Date:** 2022-06-20  
**Description:** Minor release with some breaking changes / additional features

- Added `DeletedProperty` support where column type is an `int`, and the value is a UNIX timestamp
- Fix bug with encrypted properties not handling `null` values
- **[Breaking]** - Updated minimum Umbraco dependency to v10
- **[Breaking]** - Updated UI assets to be a (RCL) Razor Compiled Library. **Be sure to clean your solution to remove old files**.

## v1.1.1
**Date:** 2022-06-08  
**Description:** Minor patch release with non breaking changes

- Added client side required / regex validation support
- Added support for nullable types when mapping property filters
- Added support for passing notification messages back from action results
- Fixed SQL escaping issue when using table names with schema prefix
- Fixed bug in range property filters when a value is `null`
- Fixed bug where save opperations would show success notification even if the save opperation failed
- Fixed bug in Data Attribute validation where `IServiceProvider` wasn't being passed through
- Fixed `null` error when searching returns no items
- Fixed deleted property filter condition not working
- Fixed bug where encrypted properties would throw exception if value was `null`

## v1.1.0
**Date:** 2022-05-03   
**Description:** Minor release with some breaking changes / additional features

- Added field views support for custom field markup in list views
- Added new consistent actions API
- Added row actions support
- Added filterable properties support
- Fixed entity picker value converter not working
- Fixed JS error when editing content due to bad null checking in the Konstrukt `redirectId` interceptor
- Depricated List View Layout support
- **[Breaking]** - Obsoleted bulk actions and menu items in favour of new actions API 
- **[Breaking]** - Moved actions, data views and cards configuration out of list views onto collections API

## v1.0.2
**Date:** 2022-04-11  
**Description:** Minor patch release with non breaking changes

- Fixed OrderBy not handling name field correctly
- Updated license warning to only display if the number of "editable" collections is exceeded
- Fixed custom connection strings not working by implementing a DB factory pattern
- Introduced `IKonstruktNodeUdiResolver` to allow content apps to resolve a different node UDI than the current page
- Fixed error being thrown by menu actions because the current section wasn't being passed through to the menu

## v1.0.1
**Date:** 2022-01-27  
**Description:** Minor patch release with non breaking changes

- Fixed bug where section/tree registration can sometimes occur twice resulting in an error.
- Removed licensing header when using a single collection.
- Fixed bug with `ORDER BY 1` causing SQL exceptions

## v1.0.0
**Date:** 2022-01-20  
**Description:** Major new release  

- Initial release
