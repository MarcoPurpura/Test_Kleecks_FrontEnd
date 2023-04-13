<template>
  <input v-model="basicInput" @change="emit()" :type="inputType"/>
</template>

<script>
export default {
    name: "BaseInput",
    props: {
        basicInputFromFather:undefined,
        inputType:{
            type: String,
            default:"text"
        }
    },
    data() {
        return {
            basicInput: this.basicInputFromFather
        }
    },
    methods:{
      emit(){
          this.emit("valueEmit",this.basicInput)
      }
    }
}
</script>

<style scoped>

</style>