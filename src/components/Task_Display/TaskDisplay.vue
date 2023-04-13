<template>
    <div>
        <h2>Task List</h2>
        <div>
            <BaseButton :type="'solid'" :style="{marginRight:'20px'}" :disabled="filter === 'all'" @click="filter = 'all'">All</BaseButton>
            <BaseButton :type="'solid'" :style="{marginRight:'20px'}" :disabled="filter === 'active'" @click="filter = 'active'">Active</BaseButton>
            <BaseButton :type="'solid'" :style="{marginRight:'20px'}" :disabled="filter === 'completed'" @click="filter = 'completed'">Completed</BaseButton>
        </div>
        <ul>
            <li v-for="(task, index) in filteredTasks" :key="index">
                <div>

                    <div v-if="task.completed">
                      <base-check-box  :task-completion="task.completed" :check-from-father="true" @checkStatus="task.completed=!task.completed"></base-check-box>
                    </div>
                    <div v-else>
                      <base-check-box :check-from-father="false" @checkStatus="task.completed=!task.completed"></base-check-box>
                    </div>
                    <div  :style="{ textDecoration: task.completed ? 'line-through' : 'none' , backgroundColor : task.completed ?'green':'red'}">
                      {{task.description }}</div>
                    <base-button @confirm="deleteTask(index)">
                        Cancella task
                    </base-button>
                </div>
                <br/>
            </li>
            <br/>
            <br/>
        </ul>
        <p> Task left: {{ activeTaskCount }}</p>
    </div>
    <Form></Form>
</template>

<script>
import BaseInput from "../BaseInput.vue";
import BaseButton from "../BaseButton/BaseButton.vue";
import Form from "../Task_Form/Form.vue";
import BaseCheckBox from "../BaseCheckBox/BaseCheckBox.vue";

export default {
    name: "TaskDisplay",
    components: {BaseCheckBox, Form, BaseButton, BaseInput},
    data() {
        return {
            tasks: JSON.parse(localStorage.getItem('tasksData')) || [],
            filter:'all'
        }
    },
    computed: {
        activeTaskCount() {
            return this.tasks.filter(task => !task.completed).length;
        },

        filteredTasks() {
          if (this.filter === 'active') {
            return this.tasks.filter(task => !task.completed)
          } else if (this.filter === 'completed') {
            return this.tasks.filter(task => task.completed)
          } else {
            return this.tasks
          }
        },
    },
    methods: {
        deleteTask(index) {
            this.tasks.splice(index, 1);
            this.saveTasksToLocalStorage();
        },
        saveTasksToLocalStorage() {
            localStorage.setItem('tasksData', JSON.stringify(this.tasks));
        },
    }
}
</script>

<style>
.completed {
    text-decoration: line-through;
}
ul {
     display: flex;
     flex-direction: row;
     flex-wrap: wrap;
     list-style: none;
     padding: 0;
     margin: 0;
 }

li {
    display: flex;
    align-items: center;
    margin: 5px;
}

label {
    min-width: 100px;
}

button {
    margin-left: 10px;
}

</style>