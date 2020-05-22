# ui5-notes

Notes and snippets for UI5 applications

# Debugging foo

## When debugging how do I know the type of a UI5 object? 

```
.getMetadata()
```

# Event handling

## Handling events on tables

### Navigating from items on a table

sap.m.Table can have a ColumnListItem on each row. This control can have a `type="Navigation"` which will render it with an arrow on the right and make the row clickable.

```
<ColumnListItem
						type="Navigation"
						press="onRowPress">
```

To grab the item pressed ID, do:

```
function (oEvent) {
  var id = oEvent.getSource().getBindingContext().getProperty("ID");
...
```

### Deleting items on a sap.m.Table

sap.m.Table has a "Delete" mode. On this mode it renders a delete button on every row. Below an example of an handler for fetching the actioned item model path. Note this is different to putting a button on the row itself as in that case the handler needs to be slightly different (code also below).

Handler for the delete event on the table (mode="Delete"):

```
onDeleteEventFired: function(oEvent) {
  var sPath = oEvent.getParameter("listItem").getBindingContext().getPath();
  ...
},
```

Handler for the press event of a button on the row:

```
onCustomDeletePressed: function(oEvent) {
  var sPath = oEvent
      .getSource()
      .getBindingContext()
      .getPath();
  // if the button is not bound to anything in the object, then you can use this
  var sPath = oEvent.getSource().getParent().getBindingContextPath();
  ...
},
```

# Formatting

## Formatting explicitly using the formatter class

```
sap.ui.define(['sap/ui/model/type/Date'], function (sapTypeDate) {

...

var oFormatter = new sapTypeDate({
  pattern: 'yyyy/MM/dd',
});
oFormatter.formatValue(myDateObject, 'string');
```

# Binding

## Binding with Date formatting

```
<Text text="{
    path: '/someDate',
    type: 'sap.ui.model.type.Date',
    formatOptions: {
      pattern: 'yyyy/MM/dd'
    }
  }" />
```

# Model

## oModel.update sends a POST instead of a PUT/merge

In the parameters object, set merge: false to send a PUT or merge: true to send a MERGE. Otherwise it will send a POST.


# Fiori

## Issue: application does not load from a tile

Situation: You have a tile with a target mapping with a Semantic object and action. The app is deployed into the backend as a BSP and everything looks good, yet when you click the tile an error is thrown at the console:

```
"text": "Error in app component com.x.y.app: No descriptor was found"
```
Or similar.

Clearing browser cache does not help. In these situations one thing that might help is running report `/UI5/APP_INDEX_CALCULATE` in se38.
Use it to reindex the files of your application.

Other options are clearing caches in the frontend server. Namely:

- Run report `/ui2/delete_cache_after_imp`
- Run transaction `/nsmicm` and go to `GOTO > HTTP plugin > Server cache > Invalidate globally`.
- Run transaction `/n/iwfnd/cache_cleanup`

## Launchpad configuration url

`https://URL_TO_FRONTEND_SERVER/sap/bc/ui5_ui5/sap/arsrvc_upb_admn/main.html`
