<template>

  <div :class="classes">

    <div class="flex xs:flex-col sm:flex-col md:flex-col lg:flex-row">

      <d-icon v-if="icon" :icon="icon" />
      <h3 v-if="title" class="font-bold">{{title}}</h3>

      <div v-if="content" class="text-sm flex-auto">{{content}}</div>

      <span class="flex-grow right">
        <slot></slot>
      </span>

    </div>

<!--
    <div class="grid sm:grid-cols-6 md:grid-cols-8 lg:grid-cols-12 gap-4">

      <d-icon v-if="icon" class="sm:col-span-2 md:col-span-2 lg:col-span-2" :icon="icon" />

      <h3 v-if="title" class="font-bold sm:col-span-4 md:col-span-6 lg:col-span-8">{{title}}</h3>

      <div v-if="content" class="text-xs sm:col-span-4 md:col-span-6 lg:col-span-10">{{content}}</div>

      <span class="sm:col-span-2 md:col-span-2 lg:col-span-2 sm:center md:right">
        <slot></slot>
      </span>

    </div>
-->


    <!-- Leave this alone: Vite doesn't recognise computed CSS -->
    <div class="alert-info alert-warning alert-success alert-error" />
  </div>

</template>

<script>

export default {

  name: 'DAlert',

  props: {

    title: {
      type: String,
      default: null,
    },

    content: {
      type: String,
      required: true,
    },

    icon: {
      type: Object,
      default: null,
    },

    type: {
      type: String,
      validator(value) {
        return ['info','success', 'warning', 'error'].includes(value)
      },
      default: null,
    },

    button: {
      type: [Object, Array],
      default: null,
    },

  },

  methods: {

  },

  computed: {
    classes: function () {
      return 'alert' + (this.type ? ' alert-' + this.type.trim().toLowerCase() : '') + ' shadow-lg'
    }
  },
}
</script>
