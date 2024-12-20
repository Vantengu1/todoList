  <template>
    <div class="app-container">
      <h1 class="app-title">To-Do list on Vue3</h1>
      <h2 class="app-subTitle">write your task, click on button "add" and look</h2>
      <TodoList
      :tasks="tasks"
      @add-task="addTask"
      @remove-task="removeTask"
      @toggle-completion="toggleTaskCompletion"
      />
    </div>
  </template>


<script>
  import TodoList from './components/TodoList.vue';
  import { ref } from 'vue';

  export default {
    name: 'App',
    components: { TodoList },
    setup() {
      const tasks = ref([]);

      const addTask = (newTask) => {
        tasks.value.push({
          id: Date.now(), // уникальный индификатор задачи
          text: newTask, // текст задачи
          completed: false, // статус выполнения
        })
      }

      const removeTask = (taskId) => {
        tasks.value = tasks.value.filter(task => task.id !== taskId);
      };

      const toggleTaskCompletion = (task) => {
        task.completed =  !task.completed;
      };

      return { tasks, addTask, removeTask, toggleTaskCompletion };
    }
  }
</script>


<style scoped>
.app-container {
  font-family: Arial, "Helvetica Neue", Helvetica, sans-serif;
  text-align: center;
  background-color: aliceblue;
  padding: 20px;
  border-radius: 10px;
  max-width: 700px;
  margin: 40px auto;
  box-shadow: 0 4px 6px black;
}

.app-title {
  font-size: 2.5rem;
  color: darkslategray;
  margin-bottom: 22px;
}

.app-subTitle {
  font-size: 1rem;
  font-weight: 200;
  color: gray;
}
</style>
