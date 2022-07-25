<template>
  <label v-if="label" :for="uuid">{{ label }}</label>
  <input
    class="field"
    v-bind="$attrs"
    :id="uuid"
    :aria-describedby="error ? `${uuid}-error` : null"
    :aria-invalid="error ? true : null"
    :placeholder="label"
    :value="modelValue"
    @input="$emit('update:modelValue', $event.target.value)"
  />
  <p
    v-if="error"
    class="errorMessage"
    aria-live="assertive"
    :id="`${uuid}-error`"
  >
    {{ error }}
  </p>
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
    error: {
      type: String,
      default: ''
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
