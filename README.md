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
