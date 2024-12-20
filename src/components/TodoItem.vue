<template>
    <li :class="{ completed: task.completed }" class="todo-item">
        <!-- the text of the task with the ability to switch the status  -->
        <span @click="$emit('toggle-completion', task)" class="task-text">
            {{ task.text }}
        </span>
        <!-- button for delete task -->
        <button @click="$emit('remove-task', task.id)" class="remove-task">Delete</button>
    </li>
</template>

<script>
export default {
    name: 'TodoItem',
    props: ['task'], //add data task
    emits: ['toggle-completion', 'remove-task'], // event advertisement for parent
};
</script>

<style scoped>
/* container for element task list */
.todo-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px;
    border-bottom: 1px solid #ddd;
}

/* styles for finish */
.completed .task-text {
    text-decoration: line-through;
    color: #aaa;
}

.task-text {
    cursor: pointer;
    flex: 0;
}

/* button delete task */
.remove-task {
    background-color: #f44336;
    color: white;
    border: none;
    border-radius: 4px;
    padding: 10px 15px;
    cursor: pointer;
    transition: background-color 0.3s;
}

.remove-task:hover {
    background-color: #e53935;
}
</style>