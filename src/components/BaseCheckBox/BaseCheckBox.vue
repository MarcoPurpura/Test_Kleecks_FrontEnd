<template>
    <label>{{title}}</label>
  <input type="checkbox" :checked="checked"  @change="handleChange"/>
</template>

<script>
export default  {
    name: "BaseCheckBox",
    props: {
        title:{
          type:String,
          default:''
        },
      checkFromFather:{
          type:Boolean,
           default: false
      },
      taskList:undefined,
      taskToChange:undefined
    },
    data() {
      return{
          checked: this.checkFromFather
      }
    },

    methods:{
        handleChange()  {
          this.checked=!this.checked
          this.$emit("checkStatus",this.checked)
        }
    }
}
</script>

<style scoped>

</style>