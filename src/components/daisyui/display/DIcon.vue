<template>
   <div class="flex">
     <component :class="classes" :is="icon" />
     <span v-if="text">&nbsp;{{text}}</span>
     <slot></slot>
   </div>
</template>

<script>

export default {

  name: 'DIcon',

  props: {

    icon: {
      type: Object,
      required: true
    },

    text: {
      type: String,
      default: null
    },

    size:{
      type: [String, Number],
      default: 6
    },

    class: {
      type: String,
      default: null
    },

  },

 computed: {
   classes: function () {
     return (this.class ? this.class + ' ' : '') + 'h-' + this.size + ' w-' + this.size
   }
 },

}
</script>
