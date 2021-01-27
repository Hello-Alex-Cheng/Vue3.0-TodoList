<template>
  <main>
    <div class="container">
      <h1>HelloAlexCc</h1>
      <todo-add :tid="todos.length" @add-todo="addTodo" />
      <todo-filter :selected="filter" @change-filter="filter = $event" />
      <todo-list :todos="filteredTodos" @delete-item="deleteTodo" />
    </div>
  </main>
</template>

<script>
import TodoAdd from "./components/TodoAdd.vue";
import TodoFilter from "./components/TodoFilter.vue";
import TodoList from "./components/TodoList.vue";
import useTodos from "@/composables/useTodos.js";
import useFilteredTodos from "@/composables/useFilteredTodos.js";

export default {
  name: "App",
  components: {
    TodoAdd,
    TodoFilter,
    TodoList,
  },
  setup() {
    // 拿到 todo 清单，以及向 todo 清单添加任务的方法
    const {todos, addTodo, deleteTodo} = useTodos()

    // filter 表示 key = ['all', 'done', 'todo']
    const {filter, filteredTodos} = useFilteredTodos(todos);

    return {
      todos,
      filter,
      addTodo,
      deleteTodo,
      filteredTodos,
    };
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: Helvetica, "PingFang SC", "Microsoft Yahei", sans-serif;
}

/* 整个页面 */
main {
  width: 100vw;
  min-height: 100vh;
  padding: 10vh 0;
  display: grid;
  align-items: start;
  justify-items: center;
  background: rgb(203, 210, 240);
}

.container {
  width: 60%;
  max-width: 400px;

  box-shadow: 0px 0px 24px rgba(0, 0, 0, 0.15);
  border-radius: 24px;
  padding: 48px 28px;
  background-color: rgb(245, 246, 252);
}

/* 标题 */
h1 {
  margin: 24px 0;
  font-size: 28px;
  color: #414873;
}
</style>
