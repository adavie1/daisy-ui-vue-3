<template>

  <!-- The button to open modal -->
  <label :for="localId" :class="buttonClass">{{openText}}</label>

  <!-- Put this part before </body> tag -->
  <input type="checkbox" :id="localId" class="modal-toggle" />

  <div class="modal modal-bottom sm:modal-middle">
    <div :class="'modal-box relative bg-' + background + ' text-' + colorText">

      <label v-if="close" :for="localId"
       :class="'btn' + ' btn-' + closeType.trim().toLowerCase() + ' btn-sm btn-circle absolute right-2 top-2 text-white'">✕</label>

      <slot :id="localId"></slot>

      <div class="modal-action">
        <label :for="localId" :class="buttonClass">{{closeText}}</label>
      </div>


    </div>
  </div>

</template>



<script>

export default {
  name: 'DModal',

  props: {
    id: {
      type: [String, Number],
    },

    openText: {
      type: String,
      default: 'Open'
    },

    close: {
      type: Boolean,
      default: true
    },

    closeType: {
      type: String,
      validator(value) {
        return ['primary', 'secondary', 'accent', 'info','success', 'warning', 'error'].includes(value)
      },
      default: 'warning'
    },


    buttonType: {
      type: String,
      validator(value) {
        return ['primary', 'secondary', 'accent', 'info','success', 'warning', 'error', 'ghost', 'link', 'active', 'disabled'].includes(value)
      },
      default: null
    },


    buttonOutline: {
      type: Boolean,
      default: false
    },

    closeText: {
      type: String,
      default: 'Close'
    },

    background: {
      type: String,
      default: 'white'
    },

    colorText: {
      type: String,
      default: 'black'
    },

  },


  computed: {
    buttonClass: function () {
      return 'btn' +  (this.buttonOutline ? ' btn-outline': '') + (this.buttonType ? ' btn-' + this.buttonType.trim().toLowerCase() : '')
    }
  },

  data () {
    return {
      localId: this.id ? this.id : Math.random()
    }
  }

}

</script>
