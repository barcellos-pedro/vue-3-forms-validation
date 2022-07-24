<template>
  <input
    type="radio"
    v-bind="$attrs"
    :id="uuid"
    :checked="modelValue === value"
    :value="value"
    @change="$emit('update:modelValue', value)"
  />
  <label v-if="label" :for="uuid">{{ label }}</label>
</template>
<script>
import UniqueID from '../features/UniqueID'

export default {
  props: {
    label: {
      type: String,
      default: ''
    },
    modelValue: {
      type: [String, Number],
      default: ''
    },
    value: {
      type: [String, Number],
      required: true
    }
  },
  setup () {
    const uuid = UniqueID().getID()
    return {
      uuid
    }
  }
}
</script>
