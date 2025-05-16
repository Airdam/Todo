<template>
  <button :type="buttonType" :class="[{ 'w-full': block }, buttonClasses[design]]">
    <slot />
  </button>
</template>

<script>
export default {
  props: {
    buttonType: {
      type: String,
      default: 'button'
    },
    design: {
      type: String,
      default: 'success'
    },
    block: {
      type: Boolean,
      default: false
    }
  },
  computed: {
    successClasses() {
      return 'rounded p-2 bg-green-500 text-white flex justify-center'
    },
    infoClasses() {
      return 'rounded p-2 bg-blue-500 text-white flex justify-center'
    },
    dangerClasses() {
      return 'rounded p-2 bg-red-500 text-white flex justify-center'
    },
    buttonClasses() {
      return {
        'success': this.successClasses,
        'info': this.infoClasses,
        'danger': this.dangerClasses,
      }
    }
  }
}
</script>

<style></style>
