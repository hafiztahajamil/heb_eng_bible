<template>
  <component
    :is="componentTag"
    class="badge"
    :class="`badge-${type}`"
    :href="href"
  >
    <slot></slot>
  </component>
</template>
<script>
export default {
  name: 'Badge',
  props: {
    tag: {
      type: String,
      default: 'span'
    },
    href: String,
    type: {
      type: String,
      default: 'default',
      validator: (value) => {
        const acceptedValues = [
          'primary',
          'info',
          'success',
          'warning',
          'danger',
          'default',
          'neutral'
        ]
        return acceptedValues.includes(value)
      }
    }
  },
  computed: {
    componentTag() {
      return this.href ? 'a' : this.tag
    }
  }
}
</script>
<style></style>
