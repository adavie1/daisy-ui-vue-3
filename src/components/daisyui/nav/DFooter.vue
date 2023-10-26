<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>

    <div :data-theme="dataTheme" class="btm-nav z-50 pb-3">

      <span v-for="(m, i) in menu" :key="i">
       <RouterLink :to="m.href">

         <div class="tooltip tooltip-top tooltip-secondary" :data-tip="m.name">

         <d-icon v-if="m.icon" :icon="m.icon" :size="iconSize">
           <div v-if="m.name && displayName">{{m.name}}</div>
         </d-icon>

        </div>

       </RouterLink>

     </span>
    </div>

</template>

<script>

export default {
  props: {
    menu: {
      type: Array,
      required: true
    },

    dataTheme: {
      type: String,
      default: 'dark'
    },

    iconSize: {
      type: [String, Number],
      default: 6
    },

    displayName: {
      type: Boolean,
      default: false
    },
  }
}
</script>
