<template>
    <div class="todo-list-container">
        <form @submit.prevent="addNewTask" class="todo-form">
            <input v-model="newTaskInput" type="text" class="todo-input" placeholder="add new task">
            <button type="submit" class="todo-button">add</button>
        </form>
        <ul class="todo-list">
            <TodoItem
            v-for="task in tasks"
            :key="task.id"
            :task="task"
            @remove-task="$emit('remove-task', $event)"
            @toggle-completion="$emit('toggle-completion', $event)"
            />
        </ul>
    </div>
</template>

<script>
import { ref } from 'vue';
import TodoItem from './TodoItem.vue';

export default {
    name: 'TodoList',
    components: { TodoItem },
    props: ['tasks'],
    emits: ['add-task', 'toggle-completion', 'remove-task'],
    setup(_, { emit }) {
        const newTaskInput = ref('');

        const addNewTask = () => {
            if (newTaskInput.value.trim() !== '') {
                emit('add-task', newTaskInput.value)
                newTaskInput.value = '';
            }
        }

        return { newTaskInput, addNewTask };
    }
}
</script>

<style scoped>
/* контейнер для списка задач */
.todo-list-container {
    max-width: 600px;
    margin: 30px auto;
    background: #fff;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 2px 4px black;
}

/* форма добавления задач */
.todo-form {
    display: flex;
    gap: 10px;
    margin-bottom: 20px;
}

.todo-input {
    flex: 1;
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 4px;
}

.todo-button {
    background-color: #447446;
    color: white;
    border: none;
    padding: 10px 20px;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s;
}

.todo-button:hover {
    background-color: #37729c;
}

/* список задач */
.todo-list {
    list-style: none;
    padding: 0;
}
</style>