# combo-box

## Props

| Prop name         | Description                                                                                                                                                                                                                                     | Type      | Values | Default   |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------- | ------ | --------- |
| label             | Label displayed above the associated form field.                                                                                                                                                                                                | string    | -      | ''        |
| description       | Description displayed below the associated form field to provide additional details about what value to enter.                                                                                                                                  | string    | -      | ''        |
| invalid           | Render field border with error color.                                                                                                                                                                                                           | boolean   | -      | false     |
| errorMessage      | Static error message displayed below the associated form field.                                                                                                                                                                                 | string    | -      | ''        |
| disabled          | Disabled state of the associated form field.                                                                                                                                                                                                    | boolean   | -      | false     |
| required          | Whether the associated form field is required or not.                                                                                                                                                                                           | boolean   | -      | false     |
| borderless        | Whether or not the associated form field is borderless.                                                                                                                                                                                         | boolean   | -      | false     |
| underlined        | Whether or not the associated form field is underlined.                                                                                                                                                                                         | boolean   | -      | false     |
| open              | Whether or not the options of the dropdown are rendered.                                                                                                                                                                                        | boolean   | -      | false     |
| options           | Collection of options for this combo box.                                                                                                                                                                                                       | array     | -      |           |
| value             | Value or Values of the selected items.                                                                                                                                                                                                          | undefined | -      | undefined |
| selectedText      | Description text of the selected items.                                                                                                                                                                                                         | string    | -      | ''        |
| readonly          | If true, the combo box is readonly.                                                                                                                                                                                                             | boolean   | -      | false     |
| multiple          | Whether the combo box allow select more than one option.                                                                                                                                                                                        | boolean   | -      | false     |
| allowFreeform     | Whether the combo box is free form, meaning that the user input is not bound to provided options.                                                                                                                                               | boolean   | -      | false     |
| autoComplete      | Whether the combo box auto completes. As the user is inputing text, it will be suggested potential matches from the list of options. If the combo box is expanded, this will also scroll to the suggested option, and give it a selected style. | boolean   | -      | false     |
| accentInsensitive | Whether the combo box ignore accent when match texts.                                                                                                                                                                                           | boolean   | -      | false     |
| placeholder       | Placeholder text rendered in the combo box.                                                                                                                                                                                                     | string    | -      | ''        |
| suggestedIndex    | Index of the suggested option.                                                                                                                                                                                                                  | number    | -      | -1        |
| optionsLoaded     | Whether the combo box must to render options or loading progress.                                                                                                                                                                               | boolean   | -      | true      |
| loadingText       | The text to display while the results are loading.                                                                                                                                                                                              | string    | -      | ''        |

## Events

| Event name | Properties | Description                                                                            |
| ---------- | ---------- | -------------------------------------------------------------------------------------- |
| input      |            | Raised when an alteration to the ComboBox's text field value is committed by the user. |
| keydown    |            | Raised when a key is pressed.                                                          |
| select     |            | Raised when an user selects an item of dropdown's Select.                              |
| click      |            | Raised when the user clicks on the caret of the ComboBox.                              |

## Slots

| Name    | Description      | Bindings                                                                                                                                                                                                                                                                                                                 |
| ------- | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| default | ComboBox's item. | **option** `object` - Option reference.<br>**index** `number` - Option's index.<br>**selected** `boolean` - Selected state of the option.<br>**marked** `boolean` - Marked state of the option.<br>**highlighted** `boolean` - Highlighted state of the option.<br>**click** `function` - Function to select the option. |

---
