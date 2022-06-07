---
description: Changelog for Konstrukt, the back office UI builder for Umbraco.
---

# Changelog

## v1.1.1
**Date:** TBC
**Description:** Minor patch release with non breaking changes

- Added client side required / regex validation support
- Added mapping support for nullable typed when mapping property filters
- Added support for passing notification messages back from action results
- Fixed SQL escaping issue when using table names with schema prefix
- Fixed bug in range property filters when a value is `null`
- Fixed bug where save opperations would show success notification even if the save opperation failed
- Fixed bug in Data Attribute validation where `IServerProvider` wasn't being passed through
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
