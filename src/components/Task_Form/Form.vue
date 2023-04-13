<template>
    <form>
        <label for="task-input">Task:</label>
        <input type="text" id="task-input" @change="checkIfValid" v-model="taskDescription" required>
        <BaseButton :type="'solid'" :disabled="enabled" @confirm="addTask" >Aggiungi Task</BaseButton>
    </form>
</template>

<script>
import BaseButton from "../BaseButton/BaseButton.vue";

export default {
    name:"Form",
    components: {BaseButton},
    data() {
        return {
            tasks: JSON.parse(localStorage.getItem('tasksData')) || [],
            taskDescription: '',
            enabled:false
        }
    },
    methods: {
        checkIfValid() {
            return this.taskDescription.trim() !== '';
        },
        addTask() {
            if (this.taskDescription.trim()) {
                this.tasks.push({ id: Date.now(),description: this.taskDescription, completed: false });
                this.saveTasks(); //salvo nel localstorage
            } else {
                //Controllo se è vuota e impedisco di seffettuare il sumbit in caso
                alert("La descrizione non può essere vuota");
            }
        },
        saveTasks() {
            localStorage.setItem('tasksData', JSON.stringify(this.tasks));
        }
    }
}
</script>

<style scoped>

</style>