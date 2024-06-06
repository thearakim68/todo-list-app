<template>
    <div class="todo-list">
        <h1>To-Do List</h1>
        <input v-model="newTask" @keyup.enter="addTask" placeholder="Add a new task">
        <select v-model="newTaskPriority">
            <option value="low">Low</option>
            <option value="medium">Medium</option>
            <option value="high">High</option>
        </select>
        <button @click="addTask" class="add-task">Add Task</button>
        <ul>
            <li v-for="task in tasks" :key="task.id">
                {{ task.text }}
                <button @click="removeTask(task.id)">Remove</button>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    data() {
        return {
            newTask: '',
            newTaskPriority: 'low',
            tasks: this.getTasksFromLocalStorage()
        }
    },
    watch: {
        tasks: {
            handler(tasks) {
                this.saveTasksToLocalStorage(tasks);
            },
            deep: true
        }
    },
    methods: {
        addTask() {
            if(this.newTask.trim()) {
                this.tasks.push({ id: Date.now(), text: this.newTask, priority: this.newTaskPriority });
                this.newTask = '';
                this.newTaskPriority = 'low';
            }
        },
        removeTask(id) {
            this.tasks = this.tasks.filter(task => task.id !== id);
        },
        saveTasksToLocalStorage(tasks) {
            localStorage.setItem('tasks', JSON.stringify(tasks));
        },
        getTasksFromLocalStorage() {
            const tasks = localStorage.getItem('tasks');
            return tasks ? JSON.parse(tasks) : [];
        }
    }
}
</script>

<style scoped>
    .todo-list {
        max-width: 600px;
        margin: 0 auto;
        padding: 20px ;
        border: 1px solid #cccc;
        border-radius: 8px;
    }
    input, select, .add-task {
        width: 100%;
        padding: 10px;
        margin-bottom: 10px;
        border-radius: 4px;
        border: 1px solid #b4b4b4;
    }
    ul {
        list-style: none;
        padding: 0;
    }
    li {
        display: flex;
        justify-content: space-between;
        padding: 10px;
        border-bottom: 1px solid #eee;
    }
    button {
        background: #ff0000;
        color: #fff;
        border: none;
        padding: 5px 10px;
        cursor: pointer;
    }
    button:hover{
        background: #cc0000;
    }
    .low {
        color: green;
    }
    .medium {
        color: orange;
    }
    .high {
        color: red;
    }
</style>