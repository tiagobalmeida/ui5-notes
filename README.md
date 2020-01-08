# ui5-notes

Notes and snippets for UI5 applications

# Event handling

## Handling events on tables

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
  ...
},
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
