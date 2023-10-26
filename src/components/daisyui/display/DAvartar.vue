<template>
  <div class="avatar">
    <div :class="classes">
     <slot></slot>
    </div>
  </div>

</template>

<script>

export default {
  name: 'DAvatar',

  props: {
    list: {
      type: Array,
      required: true
    },

    width: {
      type: [String, Number],
      default: 24
    },

    rounded: {
      type: Boolean,
      default: true
    },

  },

  methods: {
    classes () {
      return 'w-' + this.width + (this.rounded ? ' rounded' : '')
    }
  },
}

</script>
