<template>
  <component
    v-for="option in options"
    :key="option.value"
    :is="wrapperTag"
    :class="{ 'space-right': !vertical }"
  >
    <BaseRadio
      :name="name"
      :label="option.label"
      :value="option.value"
      :modelValue="modelValue"
      @update:modelValue="$emit('update:modelValue', $event)"
    />
  </component>
</template>

<script>
import BaseRadio from './BaseRadio.vue'

export default {
  components: {
    BaseRadio
  },
  props: {
    options: {
      type: Array,
      required: true
    },
    name: {
      type: String,
      required: true
    },
    modelValue: {
      type: [String, Number],
      required: true
    },
    vertical: {
      type: Boolean,
      default: false
    }
  },
  computed: {
    wrapperTag () {
      return this.vertical ? 'div' : 'span'
    }
  }
}
</script>

<style>
.space-right {
  margin-right: 20px;
}
</style>
