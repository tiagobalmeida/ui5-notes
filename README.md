# ui5-notes
Notes and snippets for UI5 applications


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
