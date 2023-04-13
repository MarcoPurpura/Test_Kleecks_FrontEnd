<template>
  <button :class="type" :disabled="disabled" :style="style" @click="showAlert($event)">
      <slot></slot>
  </button>
</template>

<script>
export default {
    name: "BaseButton",
    props: {
        style: {
          type: Object,
          default : {
            backgroundColor :'20px',
            border:'2px'
          }
        },
        type:undefined,
        disabled: {
            type: Boolean,
            default: false
        },
        nameOfReturningEmit :{
            type:String,
            default: "confirm"
        }
    },
    methods:{
        showAlert() {
            alert("Messaggio randomico");
            this.$emit(this.nameOfReturningEmit)
        }
    }
}
</script>

<style scoped>

</style>