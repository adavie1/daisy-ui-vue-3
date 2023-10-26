<script setup>
 import { HomeIcon } from '@heroicons/vue/24/outline'
</script>

<template>

<div class="text-sm breadcrumbs p-5">
  <ul>
    <li><RouterLink to="/"><HomeIcon class="h-6 w-6" /></RouterLink></li>
    <li><b>{{$route.name}}</b></li>
  </ul>
</div>

</template>


<script>

</script>
