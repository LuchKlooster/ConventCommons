# ConventCommons

Convent Commons for Mendix Ver. 1.4.0

## Module Content

- [x] [**EnumReflection**](#enumreflection) - Unlocks the full potential of enums

- [x] [**DataGrid2 - Auto-select (first) row**](#datagrid2-auto-select-first-row)

- [x] [**Gallery - Auto-select (first) row**](#gallery-auto-select-first-row)

- [x] [**DataGrid Actions**](#conventcommons--datagrid-actions) **New**

- [x] [**"User Memory"**](#user-memory)

- [x] [**Mendix Enumeration Generator**](#mendix-enumeration-generator)

- [x] [**Mendix Navigation Extractor**](#mendix-navigation-extractor)

- [x] [**Mendix Navigation CSV Import/Update**](#mendix-navigation-csv-importupdate)

## Index

- [ConventCommons](#conventcommons)
  - [Module Content](#module-content)
  - [Index](#index)
  - [Quick Implementation Guide](#quick-implementation-guide)
  - [EnumReflection](#enumreflection)
    - [How It Works](#how-it-works)
    - [Query Functions](#query-functions)
      - [GetEnumValues](#getenumvalues)
      - [GetEnumCaption](#getenumcaption)
      - [GetEnumImageName](#getenumimagename)
      - [GetEnumImage](#getenumimage)
      - [GetEnumImageURL](#getenumimageurl)
      - [GetNextEnumValue](#getnextenumvalue)
      - [GetNextMxObjectEnumValue (new in Ver. 1.2.0)](#getnextmxobjectenumvalue-new-in-ver-120)
      - [GetPrevEnumValue](#getprevenumvalue)
      - [GetPrevMxObjectEnumValue (new in Ver. 1.2.0)](#getprevmxobjectenumvalue-new-in-ver-120)
    - [Enum Mutation Functions](#enum-mutation-functions)
      - [NameToEnum](#nametoenum)
      - [CaptionToEnum](#captiontoenum)
    - [Enum Ranking](#enum-ranking)
      - [Example 1: Administrative process (Onboarding new employee)](#example-1-administrative-process-onboarding-new-employee)
      - [Example 2: Technical/Production process (Order processing)](#example-2-technicalproduction-process-order-processing)
      - [Example 3: Research Process (Step-by-Step Plan)](#example-3-research-process-step-by-step-plan)
      - [Rules](#rules)
  - [DataGrid2: Auto-Select (First) Row](#datagrid2-auto-select-first-row)
    - [Overview](#overview)
    - [The Challenge](#the-challenge)
    - [Solution Architecture](#solution-architecture)
    - [DataGrid2 Selection: How It Works](#datagrid2-selection-how-it-works)
    - [Configuration of Auto-Select Row in Mendix Studio Pro](#configuration-of-auto-select-row-in-mendix-studio-pro)
      - [Nanoflow: NF\_DG2\_SelectRow](#nanoflow-nf_dg2_selectrow)
      - [Nanoflow Setup](#nanoflow-setup)
    - [Use Cases](#use-cases)
      - [1. Page Load Event](#1-page-load-event)
      - [2. Master-Detail Grids](#2-master-detail-grids)
      - [3. Dropdown/Combobox Filtering](#3-dropdowncombobox-filtering)
  - [Gallery: Auto-Select (First) Row](#gallery-auto-select-first-row)
  - [ConventCommons — Datagrid Actions](#conventcommons--datagrid-actions)
    - [DataGrid 2 (DG2) actions](#datagrid-2-dg2-actions)
      - [Configuration of Get Filtered List in Mendix Studio Pro](#configuration-of-get-filtered-list-in-mendix-studio-pro)
      - [JA\_DG2\_GetObjectsFromGridConfig / JS\_DG2\_GetObjectsFromGridConfig](#ja_dg2_getobjectsfromgridconfig--js_dg2_getobjectsfromgridconfig)
      - [Create Column Mapping](#create-column-mapping)
      - [When to Use Java vs JavaScript](#when-to-use-java-vs-javascript)
    - [ReactDataGrid (RDG) actions](#reactdatagrid-rdg-actions)
      - [Config JSON format](#config-json-format)
      - [JS\_RDG\_BuildXPath / JA\_RDG\_BuildXPath](#js_rdg_buildxpath--ja_rdg_buildxpath)
      - [JS\_RDG\_BuildSortJSON / JA\_RDG\_BuildSortJSON](#js_rdg_buildsortjson--ja_rdg_buildsortjson)
      - [JS\_RDG\_GetObjectsFromGridConfig / JA\_RDG\_GetObjectsFromGridConfig](#js_rdg_getobjectsfromgridconfig--ja_rdg_getobjectsfromgridconfig)
      - [JS\_RDG\_GetFilteredObjects / JA\_RDG\_GetFilteredObjects](#js_rdg_getfilteredobjects--ja_rdg_getfilteredobjects)
    - [SVARdatagrid (SVAR) actions](#svardatagrid-svar-actions)
      - [Config JSON format](#config-json-format-1)
      - [JS\_SVAR\_BuildXPath / JA\_SVAR\_BuildXPath](#js_svar_buildxpath--ja_svar_buildxpath)
      - [JS\_SVAR\_BuildSortJSON / JA\_SVAR\_BuildSortJSON](#js_svar_buildsortjson--ja_svar_buildsortjson)
      - [JS\_SVAR\_GetObjectsFromGridConfig / JA\_SVAR\_GetObjectsFromGridConfig](#js_svar_getobjectsfromgridconfig--ja_svar_getobjectsfromgridconfig)
      - [JS\_SVAR\_GetFilteredObjects / JA\_SVAR\_GetFilteredObjects](#js_svar_getfilteredobjects--ja_svar_getfilteredobjects)
      - [JA\_SVAR\_ReorderRows](#ja_svar_reorderrows)
    - [TabulatorDatagrid (TAB) actions](#tabulatordatagrid-tab-actions)
      - [Config JSON format](#config-json-format-2)
      - [JS\_TAB\_BuildXPath / JA\_TAB\_BuildXPath](#js_tab_buildxpath--ja_tab_buildxpath)
      - [JS\_TAB\_BuildSortJSON / JA\_TAB\_BuildSortJSON](#js_tab_buildsortjson--ja_tab_buildsortjson)
      - [JS\_TAB\_GetObjectsFromGridConfig / JA\_TAB\_GetObjectsFromGridConfig](#js_tab_getobjectsfromgridconfig--ja_tab_getobjectsfromgridconfig)
      - [JS\_TAB\_GetFilteredObjects / JA\_TAB\_GetFilteredObjects](#js_tab_getfilteredobjects--ja_tab_getfilteredobjects)
    - [Utility actions](#utility-actions)
      - [JS\_CurrentUser / JS\_CurrentUserId](#js_currentuser--js_currentuserid)
      - [JS\_NameToEnum / JA\_NameToEnum](#js_nametoenum--ja_nametoenum)
      - [JA\_CaptionToEnum](#ja_captiontoenum)
      - [JA\_GetUserById](#ja_getuserbyid)
      - [JA\_ReorderRows](#ja_reorderrows)
    - [Filter operator reference](#filter-operator-reference)
  - ["User Memory"](#user-memory)
    - [How does it work](#how-does-it-work)
    - [Housekeeping](#housekeeping)
  - [Mendix Enumeration Generator](#mendix-enumeration-generator)
    - [Enumeration Generator Features](#enumeration-generator-features)
  - [Mendix Navigation Extractor](#mendix-navigation-extractor)
    - [Navigation Extractor Features](#navigation-extractor-features)
  - [Mendix Navigation CSV Import/Update](#mendix-navigation-csv-importupdate)
  - [License](#license)

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

### Enum Ranking

A process step enumeration is a numbered or structured list that represents the sequential actions within a workflow.
Below are examples in different contexts:

#### Example 1: Administrative process (Onboarding new employee)

- Posting a vacancy: Creating and publishing the vacancy profile.
- Job interviews: Selecting and interviewing candidates.
- Contract offer: Drafting and signing the employment contract.
- Workplace setup: Preparing the laptop, phone, and access card.
- First day of work: Reception, tour, and introductory program.
- Evaluation: Discussing performance after 30 days.

#### Example 2: Technical/Production process (Order processing)

- Receiving: The customer order is entered into the system.
- Validation: The order is checked for availability and correctness.
- Picking: Products are retrieved from the warehouse.
- Packaging: Goods are prepared for shipment.
- Shipping: The package is handed over to the carrier. Invoicing: The invoice is sent automatically.

#### Example 3: Research Process (Step-by-Step Plan)

- Problem Definition: Clearly define the topic.
- Risk Analysis: Identify potential obstacles.
- Data Collection: Gather information from relevant sources.
- Analysis: Process and interpret collected data.
- Reporting: Record conclusions in a final report.

To support these process step enumerations a set of rules is defined so you can simply ask: If orderstatus above Picking then ....

#### Rules

| Rule | Name | Logic |
| --- | --- | --- |
| A above B | AaboveB | A > B |
| A below B | AbelowB | A < B |
| A between B and C | AbetweenBandC | A > B and A < C |
| A equals B | AequalsB | A = B |
| A greater or equal B | AgeB | A >= B |
| A greater B | AgreaterB | A > B |
| A in B and C | AinBandC | A >= B and A <= C |
| A less or equal B | AleB | A <= B |
| A smaller B | AsmallerB | A < B |

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
   - `.grid-mock-header` since DataWidget ver 3.8.0 div with class .grid-mock-header is added to grid-body
   - `.tr:nth-child({datagrid2Row})` to locate the rowlect another row than first row.

**Updated: The JavaScriptAction is now compatible with DataWidget up to version 3.8.0. Mendix also has returned the auto-select first row function in version 3.8.0. You can still use the Convent Commons Auto=select (first) row in older versions or to se

### Configuration of Auto-Select Row in Mendix Studio Pro

#### Nanoflow: NF_DG2_SelectRow

| Parameter     | Type   | Description                                        |
|---------------|--------|----------------------------------------------------|
| datagrid2Name | String | Name of the DataGrid2 (without "mx-name-" prefix)  |
| datagrid2Row  | String | Row number to select (typically "1" for first row) |

#### Nanoflow Setup

Nanoflow named `NF_DG2_SelectRow` that:

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

## Gallery: Auto-Select (First) Row

The Gallery Auto-Select (First) Row is identical to the DataGrid2 Auto-Select Row.

The use of the components is similar to DataGrid; replace DataGrid2 and DG2 with Gallery.

---
---

## ConventCommons — Datagrid Actions

JavaScript Actions (JSAs) and Java Actions (JAs) that support the **DataGrid2**, **ReactDataGrid**, **SVARdatagrid** and **TabulatorDatagrid** pluggable widgets, plus general-purpose utility actions.

All grid actions read column-to-attribute mappings from the `columnMeta` block embedded in the widget's config JSON — no separate mapping document is required.

---
---
### DataGrid 2 (DG2) actions

Actions for the standard Mendix DataGrid 2 widget:

| Action | Parameters | Description |
| --- | --- | --- |
| `JS_DG2_BuildXPath` | `entityName`, `filterJSON` | Builds an XPath string from a DataGrid 2 filter JSON |
| `JA_DG2_BuildXPath` | `EntityName`, `FilterJSON` | Java equivalent |
| `JS_DG2_GetObjectsFromGridConfig` | `returnObjectType`, `gridConfigJSON` | Retrieves objects from a DG2 config JSON |
| `JA_DG2_GetObjectsFromGridConfig` | `ReturnObjectType`, `GridConfigJSON` | Java equivalent |
| `JS_DG2_SelectRow` | `datagrid2Name`, `datagrid2Row` | Programmatically selects a row in DataGrid 2 (see [DataGrid2: Auto-Select (First) Row](#datagrid2-auto-select-first-row)) |
| `JS_Gallery_SelectRow` | `galleryName`, `galleryRow` | Programmatically selects an item in a Gallery widget |

#### Configuration of Get Filtered List in Mendix Studio Pro

When a microflow or nanoflow is called via a button in a datagrid, there is only one option to pass data from the grid as a parameter:
 'Selection of >GridName<' - the **selected rows from the grid**.

However, sometimes it's desirable to retrieve not the **selected rows**, but the **filtered data** in the called flow.

#### JA_DG2_GetObjectsFromGridConfig / JS_DG2_GetObjectsFromGridConfig

This solution, available as JavaAction and as JavascriptAction, reads the stored DataGrid2 configuration JSON to automatically apply the same filters and sorting that the user sees in the grid.

JavaAction `JA_DG2_GetObjectsFromGridConfig`

JavaScript Action `JS_DG2_GetObjectsFromGridConfig`.

**No Limitations:**
All forms of Pagination can be used with this method.
This method is suitable for large amounts of data.

- **Parameters:**
  - `Return object type`: (entity) - Select the entity that is used in DG2 Data source
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

#### When to Use Java vs JavaScript

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

### ReactDataGrid (RDG) actions

#### Config JSON format

```json
{
  "sortColumns":   [{ "columnKey": "13", "direction": "ASC" }],
  "filters":       { "13": "<|5", "17": "invoice" },
  "filtersVisible": true,
  "columnOrder":   ["6","7","8","13","17"],
  "hiddenColumns": ["8"],
  "columnMeta": {
    "13": { "xpathName": "Completion",           "type": "Integer" },
    "17": { "xpathName": "Enum_Transactiontype", "type": "Enum"    }
  }
}
```

Both `filters` keys and `columnMeta` keys use the **stable numeric suffix** of the Mendix attribute ID (e.g. `attr_jge_13` → `"13"`). Filter values use the `op|value` pipe format (e.g. `"<|5"`, `"contains|smith"`); Enum and Boolean values are stored plain (`"invoice"`, `"true"`).

---
---

#### JS_RDG_BuildXPath / JA_RDG_BuildXPath

| Parameter | Type | Description |
| --- | --- | --- |
| `entityName` / `EntityName` | String | Full entity name, e.g. `MyModule.MyEntity` |
| `gridConfigJSON` / `GridConfigJSON` | String | Value of the widget's **Configuration attribute** |
| `returnFullXPath` / `ReturnFullXPath` | Boolean | `true` → `//Entity[constraints]`; `false` → `[constraints]` only |

Returns a String. Set `returnFullXPath = false` for the **XPath Marketplace module** which expects only the constraint part.

---
---

#### JS_RDG_BuildSortJSON / JA_RDG_BuildSortJSON

| Parameter | Type | Description |
| --- | --- | --- |
| `gridConfigJSON` / `GridConfigJSON` | String | Value of the widget's **Configuration attribute** |

Returns a JSON string, e.g. `[["Completion","asc"],["Name","desc"]]`. Returns `[]` when no sort is active.

---
---

#### JS_RDG_GetObjectsFromGridConfig / JA_RDG_GetObjectsFromGridConfig

| Parameter | Type | Description |
| --- | --- | --- |
| `returnObjectType` / `ReturnObjectType` | String | Full entity name, e.g. `MyModule.MyEntity` |
| `gridConfigJSON` / `GridConfigJSON` | String | Value of the widget's **Configuration attribute** |

Retrieves objects applying both filter constraints and sort order in one call. Returns `List<MxObject>`. The JS variant requires **Strict mode = No** in App Security.

---
---

#### JS_RDG_GetFilteredObjects / JA_RDG_GetFilteredObjects

| Parameter | Type | Description |
| --- | --- | --- |
| `returnObjectType` / `ReturnObjectType` | String | Full entity name, e.g. `MyModule.MyEntity` |
| `xPathConstraint` / `XPathConstraint` | String | XPath constraint string, e.g. output of `JS_RDG_BuildXPath` (may be empty) |

Retrieves objects using a plain XPath constraint. Empty string returns all objects. The JS variant requires **Strict mode = No** in App Security.

---
---

### SVARdatagrid (SVAR) actions

#### Config JSON format

```json
{
  "filtersVisible": true,
  "hiddenColumns":  ["attr_aad_14"],
  "columnWidths":   { "13": 150 },
  "sortState":      { "13": { "order": "asc", "index": 0 } },
  "filters":        { "attr_aad_13": "contains|smith", "attr_aad_14": ">=|100" },
  "columnMeta":     { "13": { "xpathName": "Name", "type": "String" } }
}
```

- **`filters` keys** are raw Mendix attribute IDs (e.g. `attr_aad_13`). Actions convert these to stable keys via `getStableKey()` before looking up `columnMeta`.
- **`sortState`, `columnMeta`, `hiddenColumns`, `columnWidths` keys** use the stable numeric suffix (e.g. `"13"`).
- **Filter values** use the `op|value` pipe format, e.g. `"contains|smith"`, `">=|100"`, `"<|50"`.

---
---

#### JS_SVAR_BuildXPath / JA_SVAR_BuildXPath

| Parameter | Type | Description |
| --- | --- | --- |
| `entityName` / `EntityName` | String | Full entity name, e.g. `MyModule.MyEntity` |
| `gridConfigJSON` / `GridConfigJSON` | String | Value of the widget's **Configuration attribute** |
| `returnFullXPath` / `ReturnFullXPath` | Boolean | `true` → `//Entity[constraints]`; `false` → `[constraints]` only |

Returns a String.

---
---

#### JS_SVAR_BuildSortJSON / JA_SVAR_BuildSortJSON

| Parameter | Type | Description |
| --- | --- | --- |
| `gridConfigJSON` / `GridConfigJSON` | String | Value of the widget's **Configuration attribute** |

Returns a JSON sort array based on `sortState`, e.g. `[["Name","asc"],["Amount","desc"]]`. Returns `[]` when no sort is active.

---
---

#### JS_SVAR_GetObjectsFromGridConfig / JA_SVAR_GetObjectsFromGridConfig

| Parameter | Type | Description |
| --- | --- | --- |
| `returnObjectType` / `ReturnObjectType` | String | Full entity name, e.g. `MyModule.MyEntity` |
| `gridConfigJSON` / `GridConfigJSON` | String | Value of the widget's **Configuration attribute** |

Retrieves objects applying filters and multi-column sort order. Returns `List<MxObject>`. The JS variant requires **Strict mode = No** in App Security.

---
---

#### JS_SVAR_GetFilteredObjects / JA_SVAR_GetFilteredObjects

| Parameter | Type | Description |
| --- | --- | --- |
| `returnObjectType` / `ReturnObjectType` | String | Full entity name, e.g. `MyModule.MyEntity` |
| `xPathConstraint` / `XPathConstraint` | String | XPath constraint string **or** full grid config JSON |

When `xPathConstraint` starts with `{` it is parsed as a SVAR grid config JSON and the XPath predicate is extracted automatically. Otherwise used as a plain XPath constraint. Empty string returns all objects.

---
---

#### JA_SVAR_ReorderRows

Renumbers a sort-order attribute after a drag-and-drop row reorder.

| Parameter | Type | Description |
| --- | --- | --- |
| `ObjectType` | String | Full entity name, e.g. `MyModule.MyEntity` |
| `SortAttribute` | String | Name of the Integer/Long sort-order attribute, e.g. `SortOrder` |
| `MovedObject` | IMendixObject | The object that was dragged |
| `SuccessorId` | String | Mendix ID string of the row now directly below the moved row; empty = moved to the last position |
| `XPathConstraint` | String | Optional XPath constraint to limit the reorder scope, e.g. `[MyAssoc = '[%CurrentObject%]']` |

Returns `Boolean` (`true` on success). Renumbers all objects in scope in steps of 10, commits only changed objects.

---
---

### TabulatorDatagrid (TAB) actions

#### Config JSON format

```json
{
  "sorters":    [{ "field": "attr_aad_6", "dir": "asc" }],
  "filters":    [{ "field": "attr_aad_6", "type": "<", "value": 100 }],
  "colLayout":  [{ "field": "attr_aad_6", "title": "ID", "width": 150, "visible": true }],
  "columnMeta": {
    "attr_aad_6":  { "xpathName": "ID_1",  "type": "Integer" },
    "attr_aad_7":  { "xpathName": "Task",  "type": "String"  },
    "attr_aad_16": { "xpathName": "Budget","type": "Decimal" }
  }
}
```

All keys (`filters[].field`, `sorters[].field`, `columnMeta` keys) use the raw Mendix attribute ID (e.g. `attr_aad_6`). No stable key conversion is needed — the keys match directly. The `type` field uses Tabulator's built-in filter operators: `=`, `!=`, `<`, `<=`, `>`, `>=`, `like`, `starts`, `ends`, `keywords`.

---
---

#### JS_TAB_BuildXPath / JA_TAB_BuildXPath

| Parameter | Type | Description |
| --- | --- | --- |
| `entityName` / `EntityName` | String | Full entity name, e.g. `MyModule.MyEntity` |
| `gridConfigJSON` / `GridConfigJSON` | String | Value of the widget's **Configuration attribute** |
| `returnFullXPath` / `ReturnFullXPath` | Boolean | `true` → `//Entity[constraints]`; `false` → `[constraints]` only |

Returns a String.

---
---

#### JS_TAB_BuildSortJSON / JA_TAB_BuildSortJSON

| Parameter | Type | Description |
| --- | --- | --- |
| `gridConfigJSON` / `GridConfigJSON` | String | Value of the widget's **Configuration attribute** |

Returns a JSON sort array based on `sorters`, e.g. `[["ID_1","asc"]]`. Returns `[]` when no sort is active.

---
---

#### JS_TAB_GetObjectsFromGridConfig / JA_TAB_GetObjectsFromGridConfig

| Parameter | Type | Description |
| --- | --- | --- |
| `returnObjectType` / `ReturnObjectType` | String | Full entity name, e.g. `MyModule.MyEntity` |
| `gridConfigJSON` / `GridConfigJSON` | String | Value of the widget's **Configuration attribute** |

Retrieves objects applying filters and sort order from the grid configuration. Returns `List<MxObject>`. The JS variant requires **Strict mode = No** in App Security.

---
---

#### JS_TAB_GetFilteredObjects / JA_TAB_GetFilteredObjects

| Parameter | Type | Description |
| --- | --- | --- |
| `returnObjectType` / `ReturnObjectType` | String | Full entity name, e.g. `MyModule.MyEntity` |
| `xPathConstraint` / `XPathConstraint` | String | XPath constraint string **or** full grid config JSON |

When `xPathConstraint` starts with `{` it is parsed as a TAB grid config JSON and the XPath predicate is built from the `filters` array and `columnMeta`. Otherwise used as a plain XPath constraint. Empty string returns all objects.

---
---

### Utility actions

#### JS_CurrentUser / JS_CurrentUserId

Returns the current logged-in user object or user ID.

#### JS_NameToEnum / JA_NameToEnum

Converts a String value to an Enum member. Useful in nanoflows/microflows where you need to construct an enum value dynamically.

#### JA_CaptionToEnum

Converts a localized enum caption back to the enum key. Useful when processing user-visible labels from a list.

#### JA_GetUserById

Retrieves a System.User object by its ID string.

#### JA_ReorderRows

Generic row reorder action (not tied to a specific widget). Renumbers a sort-order attribute for a given entity type after a drag-and-drop operation.

---
---

### Filter operator reference

All three grid widgets (RDG, SVAR, TAB) produce XPath via the same helper logic:

| Operator | Attribute type | XPath produced |
| --- | --- | --- |
| `=` | Integer/Decimal | `Attr = 100` |
| `<` | Integer/Decimal | `Attr < 100` |
| `<=` | Integer/Decimal | `Attr <= 100` |
| `>` | Integer/Decimal | `Attr > 100` |
| `>=` | Integer/Decimal | `Attr >= 100` |
| `!=` | Integer/Decimal | `Attr != 100` |
| `=` | Enum | `Attr = 'value'` |
| `=` | Boolean | `Attr = true()` |
| `contains` / `like` | String | `contains(Attr, 'value')` |
| `startsWith` / `starts` | String | `starts-with(Attr, 'value')` |
| `endsWith` / `ends` | String | `contains(Attr, 'value')` |
| `keywords` | String | `contains(Attr, 'w1') and contains(Attr, 'w2')` |
| `=` | DateTime | `Attr = dateTime('2024-01-01T00:00:00')` |
| `<` | DateTime | `Attr < dateTime('2024-01-01T00:00:00')` |

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

### Enumeration Generator Features

- [x] **Import**: Create Mendix enumerations from CSV files  
- [x] **Export**: Extract existing enumerations from Mendix projects to CSV  
- [x] **Multi-language**: Support for multiple translations per enumeration value  
- [x] **Round-trip**: Export from one project, modify, and import to another

See github [**Mendix Enumeration Generator**](https://github.com/LuchKlooster/MendixEnumerationGenerator) for details and scripts.

---
---

## Mendix Navigation Extractor

This tool extracts all navigation items from a Mendix project using the Mendix Platform SDK and Model SDK, then exports them to a CSV file.

### Navigation Extractor Features {#navigation-extractor-features}

- [x] Extracts navigation from all profiles (Desktop, Tablet, Phone)  
- [x] Captures menu items, sub-menus, and nested navigation structures  
- [x] Menu items have role information reported  
- [x] Exports home pages and role-based home pages  
- [x] Includes icon information and alternative text  
- [x] Preserves navigation hierarchy with level indicators  
- [x] Outputs to clean CSV format  

See github [**Mendix Extract Navigation**](https://github.com/LuchKlooster/MendixExtractNavigation) for details and scripts.

---
---

## Mendix Navigation CSV Import/Update

You can now **import navigation items from CSV** back into your Mendix project. This allows you to:

- [x] Create navigation menus from spreadsheets  
- [x] Bulk update navigation items  
- [x] Version control your navigation structure  
- [x] Share navigation configurations between projects  

See github [**Mendix Update Navigation**](https://github.com/LuchKlooster/MendixUpdateNavigation) for details and scripts.

---
---

## License

Apache V2 – ConventSystems B.V.
