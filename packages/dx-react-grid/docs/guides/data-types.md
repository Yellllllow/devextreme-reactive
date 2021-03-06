# Data Types

The Grid component supports custom value formatting and using a custom editor for cell value editing (depending on column's data type).

The [DataTypeProvider](../reference/data-type-provider.md) plugin holds the `for`, `formatterComponent` and `editorComponent` properties that enable you to associate the data type provider with specific columns, specify custom formatting and a custom editor.

## Related Plugins

- [DataTypeProvider](../reference/data-type-provider.md) - provides the capability to customize formatting and editors depending on the data type

## Value Formatting

Assign a function rendering the formatted value to the `DataTypeProvider` plugin's `formatterComponent` property to apply the required formatting to cells of a column associated with the specified type.

```js
const rows = [
  { product: 'SolarOne', amount: '3039' },
];
const columns = [
  { name: 'product', title: 'Product' },
  { name: 'amount', title: 'Sale Amount' },
];
const currencyColumns = ['amount'];

const CurrencyFormatter = ({ value }) => <span>${value}</span>;

<Grid
  rows={rows}
  columns={columns}
>
  <DataTypeProvider
    for={currencyColumns}
    formatterComponent={CurrencyFormatter}
  />
</Grid>
```

.embedded-demo(data-types/formatters)

## Custom Editors

If the grid supports editing or header row filtering, assign a function rendering the required editor to the `DataTypeProvider` plugin's `editorComponent` property. In this case, the Grid uses the specified editor to edit all the specified type values.

```js
const rows = [
  { product: 'SolarOne', shipped: true },
];
const columns = [
  { name: 'product', title: 'Product' },
  { name: 'shipped', title: 'Shipped' },
];
const booleanColumns = ['shipped'];

const BooleanEditor = ({ value, onValueChange }) => (
  <select
    value={value}
    onChange={e => onValueChange(e.target.value === 'true')}
  >
    <option value={false}>No</options>
    <option value>Yes</option>
  </select>
);

<Grid
  rows={rows}
  columns={columns}
>
  <DataTypeProvider
    for={booleanColumns}
    editorComponent={BooleanEditor}
  />
</Grid>
```

.embedded-demo(data-types/editors)
