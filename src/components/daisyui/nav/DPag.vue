<script setup>
import { ChevronDoubleLeftIcon, ChevronDoubleRightIcon, ChevronLeftIcon, ChevronRightIcon, Squares2X2Icon, TableCellsIcon } from '@heroicons/vue/24/solid'
</script>

<template>

  <div class="text-center max-w-full">

    <div v-if="toggleGrid" class="btn-group">

      <button class="btn" @click="firstPage"><ChevronDoubleLeftIcon  class="h-6 w-6" /></button>
      <button class="btn" @click="prevPage"><ChevronLeftIcon  class="h-6 w-6" /></button>
      <button class="btn">Page {{pg}} / {{last}}<span class="lowercase hidden md:block">&nbsp;of {{perPage}} per page</span></button>
      <button class="btn" @click="nextPage"><ChevronRightIcon  class="h-6 w-6" /></button>
      <button class="btn" @click="lastPage"><ChevronDoubleRightIcon  class="h-6 w-6" /></button>
    </div>
    <span class="pt-2 md:block" v-if="showToggle">
      &nbsp;
      <button v-if="toggleGrid" class="btn" @click="toggleChange"><TableCellsIcon class="h-6 w-6" /></button>
      <button v-else class="btn mb-2" @click="toggleChange"><Squares2X2Icon class="h-6 w-6" /></button>
    </span>

  </div>

</template>


<script>

export default {
  props: {

    total: {
      type: Number,
      required: true,
      default: 0
    },

    perPage: {
      type: Number,
      default: 10
    },

    showToggle: {
      type: Boolean,
      default: false
    },

    tableView: {
      type: Boolean,
      default: false
    }

  },


  methods: {

    toggleChange () {
      this.toggleGrid = !this.toggleGrid
      this.pageChanged ()
    },

    pageChanged () {
      this.$emit('pageChanged', this.pg, this.index, this.perPage, this.toggleGrid)
    },

    firstPage () {

      if (this.pg < this.total) {
        this.pg = 1
        this.pageChanged()
      }

    },

    nextPage () {

      if (this.pg < this.last) {
        this.pg += 1
        this.pageChanged()
      }

    },

    prevPage () {

      if (this.last > 0 && this.pg > 1) {
        this.pg -= 1
        this.pageChanged()
      }

    },

    lastPage () {

      this.pg = this.last
      this.pageChanged()

    }

  },


  computed: {
    last: function () {
      if (this.total > 0) {
        return Math.round(this.total / this.perPage, 0);
      }

    return 0
    },

    index: function () {
      if (this.total > 0) {
        return Math.round((this.pg * this.perPage) - 1, 0);
      }

    return 0
    }
  },


  data () {

    return {
      toggleGrid: !this.tableView,
      pg: (this.total > 0 ? 1 : 0)
    }

  }



}
</script>
