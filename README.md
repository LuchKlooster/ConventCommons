# ConventCommons

Convent Commons for Mendix Ver. 1.3.0


## Module Content

✅ [**EnumReflection**](#enumreflection) - Unlocks the full potential of enums

✅ [**DataGrid2 - Auto-select (first) row**](#datagrid2-auto-select-row)

✅ [**DataGrid2 - Get filtered list**](#datagrid2-get-filtered-list)  **Updated!

✅ [**"User Memory"**](#user-memory)

✅ [**Mendix Enumeration Generator**](#mendix-enumeration-generator)

✅ [**Mendix Navigation Extractor**](#mendix-navigation-extractor)  **New!

✅ [**Mendix Navigation CSV Import/Update**](#mendix-navigation-csv-import/update)  **New!


## Index
- [**Quick Implementation Guide**](#quick-implementation-guide)
- [**EnumReflection**](#enumreflection)
  - [How It Works](#how-it-works)
  - [Query Functions](#query-functions)
    - [GetEnumValues](#getenumvalues)
    - [GetEnumCaption](#getenumcaption)
    - [GetEnumImageName](#getenumimagename)
    - [GetEnumImage](#getenumimage)
    - [GetEnumImageURL](#getenumimageurl)
    - [GetNextEnumValue](#getnextmxobjectenumvalue)
    - [GetNextMxObjectEnumValue](#getnextenumvalue)
    - [GetPrevEnumValue](#getprevenumvalue)
    - [GetPrevMxObjectEnumValue](#getprevmxobjectenumvalue)
  - [Enum Mutation Functions](#enum-mutation-functions)
    - [NameToEnum](#nametoenum)
    - [CaptionToEnum](#captiontoenum)
- [**DataGrid2 - Auto-select (first) row**](#datagrid2-auto-select-row)
  - [Overview](#overview)
  - [The Challenge](#the-challenge)
  - [Solution Architecture](#solution-architecture)
  - [DataGrid2 Selection: How It Works](#datagrid2-selection-how-it-works)
  - [Configuration of Auto-Select Row in Mendix Studio Pro](#configuration-of-auto-select-row-in-mendix-studio-pro)
  - [Use Cases](#use-cases)
- [**DataGrid2 - Get Filtered List**](#datagrid2-get-filtered-list)
  - [Configuration of Get Filtered List in Mendix Studio Pro](#configuration-of-get-filtered-list-in-mendix-studio-pro)
  - [Method 1](#method-1)
  - [Method 2](#method-2)
- [**"User Memory"**](#user-memory)
  - [How does it work](#how-does-it-work)
  - [Housekeeping](#housekeeping)
- [**Mendix Enumeration Generator**](#mendix-enumeration-generator)
- [**Mendix Navigation Extractor**](#mendix-navigation-extractor)
- [**Mendix Navigation CSV Import/Update**](#mendix-navigation-csv-import/update)


## Quick Implementation Guide

1. Import the ConventCommons.mpk module into your app.
2. DataGrid2 and "User Memory" features can be used out of the box.
3. To use EnumReflection, add the microflow `ASU_EnumReflection` to your start-up microflow.
4. Optionally add the page 'Enumerations_Overview' to your navigation for insight into reflection data.
5. You're ready to use the microflows, nanoflows, and Java/JavaScript Actions in the Enumerations folders.
6. For housekeeping add the microflow `DSB_CleanShadowUser` to your before shutdown microflow.

---
---


## EnumReflection

Over the years, questions about enumerations have regularly appeared on the forum, along with answers providing partial solutions:

- CommunityCommons offers a template (EnumerationFromString) that requires a customized Java version for each enum.
- There's module EnumToList. This module allows to transform an enumeration (as object attribute) into a list of object in order to iterate with a loop.
- ModelReflection contains enum data, but not all aspects are included.
- All enum information can be found in the MetaData. Unfortunately, in recent Mendix versions, this data is not available in the client (JavaScript).

So the (partly)solutions are scattered over a handfull of modules and require high-code alterations.
I searched for the most low-code solution possible and came up with the idea of EnumReflection.  


### How It Works

In an after start-up microflow (`ASU_EnumReflection`), the JavaAction `CreateMxObjectEnum` is executed. This JavaAction searches the MetaData and stores the found data in the entities `MxObjectEnum`, `MxObjectEnumValue`, and `MxObjectEnumCaption`.

These entities, attributes, and associations can be used directly—they are normal Mendix objects. Convenience microflows and nanoflows are also available to query this data. Additionally, there are Java and JavaScript Actions to modify enum values in an object. For those who want to view the data, there's a page called `Enumerations_Overview`.


### Query Functions


#### GetEnumValues

- **Parameter:**
  - `EnumName` - Full enum name (module.enumname like system.language)
- **Result:** List of `MxObjectEnumValue` with all values of the requested enum
- **Purpose:** To loop over all values of the enum. In the iteration, all data is available in the attributes of `MxObjectEnumValue`

#### GetEnumCaption

- **Parameters:**
  - `EnumName` - Full enum name (module.enumname like system.language)
  - `EnumValue`
  - `LanguageCode` - In the format en_US, nl_NL
- **Result:** Caption associated with `EnumValue` and `LanguageCode`

#### GetEnumImageName

- **Parameters:**
  - `EnumName` - Full enum name (module.enumname like system.language)
  - `EnumValue`
- **Result:** ImageName associated with `EnumValue`

#### GetEnumImage

- **Parameters:**
  - `EnumName` - Full enum name (module.enumname like system.language)
  - `EnumValue`
  - `Enum_ImageEmbedding` - HTML or XML
- **Result:** Image associated with `EnumValue`

#### GetEnumImageURL

- **Parameters:**
  - `EnumName` - Full enum name (module.enumname like system.language)
  - `EnumValue`
- **Result:** ImageURL associated with `EnumValue`

#### GetNextEnumValue

- **Parameters:**
  - `EnumName` - Full enum name (module.enumname like system.language)
  - `EnumValue`
- **Result:** NextEnumValue or if no next value, empty string

#### GetNextMxObjectEnumValue (new in Ver. 1.2.0)

- **Parameters:**
  - `EnumName` - Full enum name (module.enumname like system.language)
  - `EnumValue`
- **Result:** Next_MxObjectEnumValue or if no next value, empty object

#### GetPrevEnumValue
- **Parameters:**
  - `EnumName` - Full enum name (module.enumname like system.language)
  - `EnumValue`
- **Result:** PrevEnumValue or if no previous value, empty string

#### GetPrevMxObjectEnumValue (new in Ver. 1.2.0)

- **Parameters:**
  - `EnumName` - Full enum name (module.enumname like system.language)
  - `EnumValue`
- **Result:** Prev_MxObjectEnumValue or if no previous value, empty object


### Enum Mutation Functions


#### NameToEnum

- **Parameters:**
  - `ObjectToChange` - MxObject
  - `AttributeName` - as string
  - `ValueAsString` - Key/Name as string
- **Result:** Attribute in Object receives the enum value corresponding to Value

#### CaptionToEnum

- **Parameters:**
  - `ObjectToChange` - MxObject
  - `EnumName` - Full enum name (module.enumname like system.language)
  - `AttributeName` - as string
  - `ValueAsString` - Caption as string
- **Result:** Attribute in Object receives the enum value corresponding to Value

**Note:**
For the Enum Mutation Functions it is necessary to make a copy of the template function.
In the copied function you need to replace the placeholder entity (MxObject System.User) with the entity that has the enum to change as an attribute.
This is because the Mendix Modeler cannot handle abstract entities, but wants an explicit entity.

---
---


## DataGrid2: Auto-Select (First) Row


### Overview

A common request in Mendix development is to automatically select the first row in a DataGrid2 after data changes. While the predecessor of DataGrid2 had this functionality built-in, it's notably absent in the current version. ConventCommons provides a JavaScript-based solution to automatically select a row in DataGrid2.


### The Challenge

The main technical challenge is that the clickable class on DataGrid2 rows is not immediately available when the page loads. The class is added asynchronously after the `mx.addOnLoad` function executes, requiring a delayed execution approach.


### Solution Architecture

The solution consists of four components:

1. **JavaScript Action** - Core logic to select a row
2. **Nanoflow** - Wrapper to execute the JavaScript Action
3. **Event Handler** - Trigger mechanism (page load)
4. **Widgets On Event Handlers** - Trigger mechanism (selection change, etc.)


### DataGrid2 Selection: How It Works

1. **Polling Mechanism:** Checks every 100ms until the gridtable is found
2. **Polling Mechanism:** Checks every 100ms until the clickable class is found
3. **Row Selection:** Simulates a click on the specified row
4. **CSS Selectors:** Uses:
   - `.mx-name-{datagrid2Name}` to locate the grid
   - `.widget-datagrid-grid-body` to locate the grid body
   - `.tr:nth-child({datagrid2Row})` to locate the row
   - `.clickable` to locate the first clickable element in the row


### Configuration of Auto-Select Row in Mendix Studio Pro


#### Nanoflow: NF_DG2_SelectRow

| Parameter     | Type   | Description                                        |
|---------------|--------|----------------------------------------------------|
| datagrid2Name | String | Name of the DataGrid2 (without "mx-name-" prefix)  |
| datagrid2Row  | String | Row number to select (typically "1" for first row) |


#### Nanoflow Setup

Create a nanoflow named `NF_DG2_SelectRow` that:

1. Accepts the same parameters as the JavaScript Action
2. Calls the `JS_DG2_SelectRow` JavaScript Action
3. Passes through the parameters


### Use Cases


#### 1. Page Load Event

Use a Page Event widget (from Marketplace) to trigger selection when a page opens.

Configuration:

- **Event:** On Load
- **Action:** Call nanoflow `NF_DG2_SelectRow`
- **Parameters:**
  - `datagrid2Name`: Enter grid name (e.g., "myDataGrid")
  - `datagrid2Row`: "1" (or desired row number)


#### 2. Master-Detail Grids

When a DataGrid2 listens to another grid (master-detail pattern).

Configuration:

- **Widget:** Master DataGrid2
- **Event:** On Selection Change
- **Action:** Call nanoflow `NF_DG2_SelectRow`
- **Target:** Detail grid name


#### 3. Dropdown/Combobox Filtering

When a DataGrid2 is filtered by a dropdown selection.

Configuration:

- **Widget:** Dropdown/Combobox
- **Event:** On Change
- **Action:** Call nanoflow `NF_DG2_SelectRow`
- **Target:** Filtered grid name

---
---


## DataGrid2: Get Filtered List

When a microflow or nanoflow is called via a button in a datagrid, there is only one option to pass data from the grid as a parameter:
 'Selection of >GridName<' - the **selected rows from the grid**.

However, sometimes it's desirable to retrieve not the **selected rows**, but the **filtered data** in the called flow.
This is now possible in two solutions using different technics.

1. using data from the displayed page, **method 1**
2. via xpath constructed from the configuration of the data grid, **method 2**


### Configuration of Get Filtered List in Mendix Studio Pro

1. Create a copy of the template JavaScriptAction/JavaAction.
2. Place the copy in your own module.
3. On the 'Settings'/'General' tab under 'Return', select the entity that is also used in the datagrid.
4. Call your copy of the JavaScriptAction/JavaAction in your Nanoflow/Microflow where you need the objectlist.
5. Only for method 2: On the 'Behavior' tab of DataGrid2, set Pagination to 'Virtual scrolling' and Page size to '999999999'.


### Method 1

JavaScript Action `JS_DG2_GetFilteredList`.

**Important Limitation:**  
In the client, only data from the displayed page is available.
This limitation can be circumvented by setting Pagination to 'Virtual scrolling' and making the page length larger than the expected number of rows.
In other words, all rows must fit on one page.

As result a list of MxObjects of type used in the DataGrid2 is desired. So we have to explicit name the entity type.
That forces us to make a copy of the JavaScript Action.
No code changes are required, just the choice of entity type has to be changed.

**Note:**  
This solution is only recommended with small amounts of data (up to 10.000 rows). For larger amounts of data a server-side solution (Method 2 JavaAction) is a better solution.


#### JS_DG2_GetFilteredList

- **Parameter:** (string) - `datagrid2Name`
- **Result:** MxObjectList
- **Prerequisite:** Pagination: Virtual scrolling and a high Page size (e.g., 999999999)


### Method 2

This approach, available as JavaAction and as JavascriptAction,  reads the stored DataGrid2 configuration JSON to automatically apply the same filters and sorting that the user sees in the grid.

JavaAction `JA_DG2_GetObjectsFromGridConfig`

JavaScript Action `JS_GetObjectsFromGridConfig`.

**No Limitations:**
The limitation from method 1 don't apply here, so all forms of Pagination can be used with this method.
This method is suitable for large amounts of data.


#### JA_DG2_GetObjectsFromGridConfig / JA_DG2_GetObjectsFromGridConfig

- **Parameters:**
  - `EntityName`: (String) - Enter entity name (e.g., "System.User")
  - `GridConfigJSON`: (String) - The Data Grid 2 configuration JSON (e.g $DataGridConfig_NP/Configuration)
  - `ColumnMapping`: (String) - JSON mapping of column IDs to attributes
- **Result:** MxObjectList


#### Create Column Mapping

You need to map column IDs (0, 1, 2...) to your attribute names.

**Example:** If your Data Grid 2 has columns:
- Column 0: Name
- Column 1: Age  
- Column 2: Status
- Column 3: CreatedDate

Create this mapping:
```json
{
  "0": "Name",
  "1": "Age",
  "2": "Status",
  "3": "CreatedDate"
}
```

#### When to Use Java vs JavaScript:

**Use JavaAction when:**
- Processing large datasets (thousands of objects)
- Need server-side security
- Part of complex server-side logic
- Need transaction control

**Use JavaScriptAction when:**
- Client-side processing (in nanoflows)
- Need to run in offline apps
- Working with UI state
- Lighter, simpler operations

---
---


## "User Memory"


"User Memory" refers to a set of features that record user choices and selections. This allows users to return to a page and see the exact same display as the last time they visited.


### How does it work

A ShadowUser is created for each visitor using the NF_GetShadowUser nanoflow.This also works for anonymous users.

To record the selection made in a ComboBox, an association is created between the Entity Attribute and the ShadowUser entity.

DataGrid2 and Gallery have a Configuration block on the Personalization tab. Here, we select as Attribute the attribute Configuration from the DataGridConfig entity. This entity is made available via a DataView with the NF_GetDG2Config nanoflow as the data source.


### Housekeeping

Especially if the app has anonymous users, we'll eventually end up with a lot of invalid ShadowUsers. To clean these up, we have the Microflow BSD_CleanShadowUser. By adding this to the before-shutdown microflow, it will automatically clean up when the app is shut down.

---
---


## Mendix Enumeration Generator


Generate Mendix SDK TypeScript code to create enumerations from CSV files, and export existing enumerations back to CSV format.


### Features

✅ **Import**: Create Mendix enumerations from CSV files  
✅ **Export**: Extract existing enumerations from Mendix projects to CSV  
✅ **Multi-language**: Support for multiple translations per enumeration value  
✅ **Round-trip**: Export from one project, modify, and import to another

See github [**Mendix Enumeration Generator**](https://github.com/LuchKlooster/MendixEnumerationGenerator) for details and scripts.

---
---


## Mendix Navigation Extractor


This tool extracts all navigation items from a Mendix project using the Mendix Platform SDK and Model SDK, then exports them to a CSV file.


### Features

✅ Extracts navigation from all profiles (Desktop, Tablet, Phone)  
✅ Captures menu items, sub-menus, and nested navigation structures  
✅ Menu items have role information reported  
✅ Exports home pages and role-based home pages  
✅ Includes icon information and alternative text  
✅ Preserves navigation hierarchy with level indicators  
✅ Outputs to clean CSV format  

See github [**Mendix Extract Navigation**](https://github.com/LuchKlooster/MendixExtractNavigation) for details and scripts.

---
---


## Mendix Navigation CSV Import/Update


You can now **import navigation items from CSV** back into your Mendix project. This allows you to:


✅ Create navigation menus from spreadsheets  
✅ Bulk update navigation items  
✅ Version control your navigation structure  
✅ Share navigation configurations between projects  

See github [**Mendix Update Navigation**](https://github.com/LuchKlooster/MendixUpdateNavigation) for details and scripts.

---
---
