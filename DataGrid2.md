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
