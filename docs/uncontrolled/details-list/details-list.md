# details-list

## Props

| Prop name        | Description                                                  | Type    | Values                       | Default         |
| ---------------- | ------------------------------------------------------------ | ------- | ---------------------------- | --------------- |
| columns          | Column defitions.                                            | array   | -                            |                 |
| data             | The items to render.                                         | array   | -                            |                 |
| groups           | Grouping instructions.                                       | array   | -                            | []              |
| selectedIndices  | Indices of the selected rows.                                | array   | -                            | []              |
| auto             | Whether the column width algorithm is set to auto or static. | boolean | -                            | false           |
| fullAuto         | Whether the table width algorithm is set to auto or full.    | boolean | -                            | false           |
| compact          | Whether to render in compact mode.                           | boolean | -                            | false           |
| selection        | Controls how/if the details list manages selection.          | string  | `multiple`, `simple`, `safe` | ''              |
| collapsible      | Whether the table groups are collapsible or not.             | boolean | -                            | false           |
| collapsedIndices | Indices of the collapsed groups.                             | Set     | -                            | () => new Set() |

## Events

| Event name         | Type | Description                                         |
| ------------------ | ---- | --------------------------------------------------- |
| click-select-all   |      | Raised when the user clicks on the header row.      |
| click-expand-all   |      | Raised when the user clicks on the header expander. |
| click-header       |      | Raised when the user clicks on a column header.     |
| click-expand       |      | Raised when the user clicks on a group expander.    |
| click-select-group |      | Raised when the user clicks on a group row.         |
| click-select-row   |      | Raised when the user clicks on a data row.          |

---