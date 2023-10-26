<template>
  <label :id="id" :class="classType" @click="(url || routerTo || routerBack) ? clicked() : null">
    <slot v-if="!(loading || text)"></slot>
    <span v-else>{{text}}</span>
  </label>

  <!-- Leave this alone: Vite doesn't recognise computed CSS -->
  <div class="btn-info btn-warning btn-success btn-error btn-secondary btn-accent btn-ghost btn-link btn-active btn-disabled btn-outline btn-glass" />

</template>

<script>

export default {
  name: 'DButton',

  props: {
    type: {
      type: String,
      validator(value) {
        return ['primary', 'secondary', 'accent', 'info','success', 'warning', 'error', 'ghost', 'link', 'active', 'disabled'].includes(value)
      },
      default: null
    },

    text: {
      type: String,
      default: null
    },

    disabled: {
      type: Boolean,
      default: false
    },

    responsive: {
      type: Boolean,
      default: false
    },

    size: {
      type: String,
      validator(value) {
        return ['xs', 'sm', 'md', 'lg'].includes(value)
      },
      default: null
    },

    glass: {
      type: Boolean,
      default: false
    },

    outline: {
      type: Boolean,
      default: false
    },

    block: {
      type: Boolean,
      default: false
    },

    circle: {
      type: Boolean,
      default: false
    },

    loading: {
      type: Boolean,
      default: false
    },

    square: {
      type: Boolean,
      default: false
    },

    routerTo: {
      type: String,
      default: null
    },

    routerBack: {
      type: Boolean,
      default: false
    },

    url: {
      type: String,
      default: null
    },

  },

  computed: {

    classType: function () {
//      console.log('type', this.type)
      return 'btn'
       + (this.type ? ' btn-' + this.type : '')
       + (this.glass ? ' glass' : '')
       + (this.outline ? ' outline' : '')
       + (this.disabled ? ' btn-disabled' : '')
       + (this.circle ? ' btn-circle' : '')
       + (this.block ? ' btn-block' : '')
       + (this.loading ? ' loading' : '')
       + (this.square ? ' btn-square' : '')
       + (this.size ? ' btn-' + this.size : '')
       + (this.responsive ? ' btn-xs sm:btn-sm md:btn-md lg:btn-lg' : '')
    },

  },



  methods: {

    clicked () {

      if (this.routerBack) {
        this.$router.back()
      }

      if (this.routerTo) {
        this.$router.push(this.routerTo)
      }

    },
  },

  data () {
    return {
      id: Math.random(),
    }
  }

}
</script>
