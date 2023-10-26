<template>

    <label :class="classes">
    <input class="hidden" type="checkbox" />
    <div v-if="onText && !onIcon" :class="onSwap" @click="changed(true)">{{onText}}</div>
    <div v-if="offText && !offIcon" :class="offSwap" @click="changed(false)">{{offText}}</div>
    <div v-if="onIcon" :class="onSwap"  @click="changed(true)"><d-icon :icon="onIcon" :size="size" /></div>
    <div v-if="offIcon" :class="offSwap" @click="changed(false)"><d-icon :icon="offIcon" :size="size" /></div>
  </label>

</template>

<script>

export default {
  name: 'DSwap',

  props: {

    modelValue:  {
      type: Boolean,
      default: false
    },

    onText: {
      type: String,
      default: null
    },

    offText: {
      type: String,
      default: null
    },

    onIcon: {
      type: Object,
      default: null
    },

    offIcon: {
      type: Object,
      default: null
    },

    flip:  {
      type: Boolean,
      default: false
    },

    rotate:  {
      type: Boolean,
      default: false
    },

    circle:  {
      type: Boolean,
      default: false
    },

    size: {
      type: [String, Number],
      default: 12
    },

    disabled: {
      type: Boolean,
      default: false
    },

  },

  computed: {
    classes:function () {
      return (this.circle ? 'btn btn-circle ' : '')
      + 'swap'
      + (this.rotate && !this.disabled ? ' swap-rotate': '')
      + (this.flip && !this.disabled ? ' swap-flip' : '')
    },

    onSwap: function () {
      return (this.disabled ? 'cursor-default' : 'swap-on')
    },

    offSwap: function () {
      return (this.disabled ? 'cursor-default' : 'swap-off')
    },

  },

  methods: {

    changed (val) {
      if (!this.disabled) {
        this.$emit('update:modelValue', (this.flip ? !val : val))
        }
    },

  },


}
</script>
