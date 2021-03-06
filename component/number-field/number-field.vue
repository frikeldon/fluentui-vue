<script>
import TextField from '../text-field'

function defaultParse (text) {
  return text === ''
    ? null
    : Number(
      text
        .replace(/(?:€|%)$/g, '')
        .replace(/\./g, '')
        .replace(',', '.')
    )
}

function defaultStringify (number) {
  if (number == null) return ''

  const options = {
    style: this.formatStyle,
    currency: 'EUR',
    useGrouping: this.useGrouping,
    minimumIntegerDigits: this.minimumIntegerDigits,
    minimumFractionDigits: this.minimumFractionDigits,
    maximumFractionDigits: this.maximumFractionDigits
  }

  if (this.minimumSignificantDigits > 0 && this.minimumSignificantDigits < 22) {
    options.minimumSignificantDigits = this.minimumSignificantDigits
  }

  if (this.maximumSignificantDigits > 0 && this.maximumSignificantDigits < 22) {
    options.maximumSignificantDigits = this.maximumSignificantDigits
  }

  const normalizedNum = this.formatStyle === 'percent' ? number / 100 : number
  return normalizedNum.toLocaleString('ca-ES', options)
}

export default {
  components: { TextField },
  props: {
    /** Label displayed above the associated form field. */
    label: { type: String, default: '' },
    /** Description displayed below the associated form field to provide additional details about what value to enter. */
    description: { type: String, default: '' },
    /** Render field border with error color. */
    invalid: { type: Boolean, default: false },
    /** Static error message displayed below the associated form field. */
    errorMessage: { type: String, default: '' },
    /** Disabled state of the associated form field. */
    disabled: { type: Boolean, default: false },
    /** Whether the associated form field is required or not. */
    required: { type: Boolean, default: false },
    /** Whether or not the associated form field is borderless. */
    borderless: { type: Boolean, default: false },
    /** Whether or not the associated form field is underlined. */
    underlined: { type: Boolean, default: false },
    /** Placeholder text rendered in the text field. */
    placeholder: { type: String, default: '' },
    /** Prefix displayed before the text field contents. This is not included in the value. */
    prefix: { type: String, default: '' },
    /** Suffix displayed after the text field contents. This is not included in the value. */
    sufix: { type: String, default: '' },
    /** Whether or not the text field is a multiline text field. */
    multiline: { type: Boolean, default: false },
    /** The name of the icon to use from the icon font. */
    icon: { type: String, default: '' },
    /** If true, the text field is readonly. */
    readonly: { type: Boolean, default: false },
    /** Maximum length (number of characters) of value. */
    maxlength: { type: Number, default: -1 },
    /** For multiline text fields, whether or not the field is resizable. */
    unresizable: { type: Boolean, default: false },
    /** For multiline text fields, whether or not to auto adjust text field height. */
    autoAdjustHeight: { type: Boolean, default: false },
    /** Current value of the number field. */
    modelValue: { type: Number, default: null },
    /**
     * The number formatting style to use.
     * @values decimal, currency, percent, unit
     */
    formatStyle: {
      type: String,
      default: 'decimal',
      validator: value => ['decimal', 'currency', 'percent', 'unit'].includes(value)
    },
    /** Whether to use grouping separators, such as thousands separators or thousand/lakh/crore separators. */
    useGrouping: { type: Boolean, default: false },
    /** The minimum number of integer digits to use. Possible values are from 1 to 21. */
    minimumIntegerDigits: {
      type: Number,
      default: 1,
      validator: value => Number.isInteger(value) && value >= 1 && value <= 21
    },
    /** The minimum number of fraction digits to use. */
    minimumFractionDigits: {
      type: Number,
      default: 0,
      validator: value => Number.isInteger(value) && value >= 0 && value <= 20
    },
    /** The maximum number of fraction digits to use. */
    maximumFractionDigits: {
      type: Number,
      default: 20,
      validator: value => Number.isInteger(value) && value >= 0 && value <= 20
    },
    /** The maximum number of fraction digits to use. */
    minimumSignificantDigits: {
      type: Number,
      default: 0,
      validator: value => Number.isInteger(value) && value >= 0 && value <= 21
    },
    /** The maximum number of significant digits to use. */
    maximumSignificantDigits: {
      type: Number,
      default: 0,
      validator: value => Number.isInteger(value) && value >= 0 && value <= 21
    },
    /** Function for convert string value to a numeric value. */
    parse: { type: Function, default: defaultParse },
    /** Function for convert numeric value to a string value. */
    stringify: { type: Function, default: defaultStringify },
    /**
     * Text align when NumberField has no focus
     * values left, center, right
     */
    align: {
      type: String,
      default: 'left',
      validator: value => ['left', 'center', 'right'].includes(value)
    },
    /**
     * Text align when NumberField has focus
     * values left, center, right
     */
    alignFocus: {
      type: String,
      default: 'left',
      validator: value => ['left', 'center', 'right'].includes(value)
    }
  },
  emits: [
    /** Raised when the value of TextField has been changed. */
    'update:modelValue',
    /** Raised when the user clicks on the icon of TextField. */
    'click'
  ],
  data () {
    return { hasFocus: false }
  },
  computed: {
    textValue: {
      get () {
        const { hasFocus, modelValue } = this
        if (hasFocus) {
          return typeof modelValue === 'number' && !isNaN(modelValue)
            ? String(modelValue)
            : ''
        } else {
          return this.stringify(modelValue)
        }
      },
      set (value) {
        if (!value) {
          this.$emit('update:modelValue', null)
        } else if (this.hasFocus) {
          this.$emit('update:modelValue', Number(value))
        } else {
          this.$emit('update:modelValue', this.parse(value))
        }
      }
    },
    textAlign () {
      const { hasFocus, align, alignFocus } = this
      return hasFocus
        ? alignFocus
        : align
    }
  },
  methods: {
    handleFocus () {
      this.hasFocus = true
    },
    handleBlur () {
      this.hasFocus = false
    },
    handleKeyDown (event) {
      const { target, key } = event
      const allowedKeys = ['Backspace', 'Delete', 'Enter', 'Tab', 'Escape', 'ArrowLeft', 'ArrowUp', 'ArrowRight', 'ArrowDown', 'Home', 'End']
      if (!allowedKeys.includes(key)) {
        const { value, selectionStart, selectionEnd } = target
        const newValue = value.substring(0, selectionStart) + key + value.substring(selectionEnd)
        if (isNaN(newValue)) {
          event.preventDefault()
          event.stopPropagation()
          event.target.value = this.textValue
        }
      }
    }
  }
}
</script>

<template>
  <TextField
    ref="textField"
    :class="textAlign"
    :label="label"
    :description="description"
    :invalid="invalid"
    :error-message="errorMessage"
    :disabled="disabled"
    :required="required"
    :borderless="borderless"
    :underlined="underlined"
    :placeholder="placeholder"
    :prefix="prefix"
    :sufix="sufix"
    :multiline="multiline"
    :icon="icon"
    :readonly="readonly"
    :maxlength="maxlength"
    :unresizable="unresizable"
    :auto-adjust-height="autoAdjustHeight"
    v-model:model-value="textValue"
    @click="$emit('click')"
    @focus="handleFocus"
    @blur="handleBlur"
    @keydown="handleKeyDown"
  />
</template>

<style scoped lang="less" src="./number-field.less" />
