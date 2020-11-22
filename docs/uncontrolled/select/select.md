# select

## Props

| Prop name        | Description                                          | Type      | Values | Default   |
| ---------------- | ---------------------------------------------------- | --------- | ------ | --------- |
| options          | Collection of options for this select.               | array     | -      |           |
| modelValue       | Value or Values of the selected items.               | undefined | -      | undefined |
| disabled         | Disabled state of the associated form field.         | boolean   | -      | false     |
| readonly         | If true, the text field is readonly.                 | boolean   | -      | false     |
| multiple         | Whether the field allow select more than one option. | boolean   | -      | false     |
| markedIndex      | Index of the marked item.                            | number    | -      | -1        |
| highlightedIndex | Index of the highlighted item.                       | number    | -      | -1        |

## Events

| Event name        | Type      | Description                                                                     |
| ----------------- | --------- | ------------------------------------------------------------------------------- |
| update:modelValue | undefined | Raised when an alteration to the Select field's value is committed by the user. |
| keydown           | undefined | Raised when a key is pressed.                                                   |

---