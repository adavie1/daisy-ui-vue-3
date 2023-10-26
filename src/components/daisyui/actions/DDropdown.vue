<template>
  <div :class="classes">

    <label :tabindex="id" class="btn m-1">{{text}}</label>

    <ul v-if="dropdown" :tabindex="id" class="dropdown-content menu p-2 shadow bg-base-300 rounded-box w-52">
      <li v-for="(m, i) in dropdown" :key="i">
        <a @click="changed(m.value, m)">{{m.label}}</a>
      </li>
    </ul>

    <div v-else :tabindex="id" class="dropdown-content">
      <slot></slot>
   </div>

  </div>

</template>

<script>

export default {
  name: 'DDropdown',

  props: {

    modelValue:  {
      type: [String, Number],
    },

    text:  {
      type: String,
      required: true
    },

    dropdown: {
      type: Array,
      default: null
    },

    position: {
      type: String,
      validator(value) {
          return ['top', 'bottom', 'left', 'right'].includes(value)
      },
      default: null
    },

    end: {
      type: Boolean,
      default: false
    },

    hover: {
      type: Boolean,
      default: false
    },

    open: {
      type: Boolean,
      default: false
    },

  },


  computed: {
    classes: function () {
      return 'dropdown '
      + (this.position && !this.hover && !this.open ? ' dropdown-' + this.position.toLowerCase() : '')
      + (this.end && !this.hover && !this.open ? ' dropdown-end' : '')
      + (this.hover && !this.open ? ' dropdown-hover' : '')
      + (this.open ? ' dropdown-open' : '')
    }
  },


  methods: {

    changed (val, obj = null) {
      this.val = val
      this.$emit('update:modelValue', this.val)

      if (obj) {
        this.$emit('changed', obj)
      }

    },

  },

  data () {
    return {
      id: Math.random(),
      val: this.value,
    }
  },

}
</script>
