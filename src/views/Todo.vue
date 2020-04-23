<template>
  <div id="todo-example">
    <fieldset>
      <legend>todo</legend>
      <!-- 上半部分 -->
      <form action @submit.prevent="addNewTodo">
        <span class="all-selected" @click="allSelected">全选</span>
        <input
          class="import-title"
          type="text"
          id="new-todo"
          :value="newTodoText"
          @input="changeText"
          placeholder="做什么好？"
          autocomplete="off"
        />
        <button class="submit-title" @submit.prevent="addNewTodo">上传</button>
      </form>
      <!-- 下半部分 -->
      <todo-item
        v-for="(todo,index) in filterTodo"
        :key="todo.id"
        @remove="changeTodos(index)"
        :todo="todo"
      ></todo-item>
      <!-- 选项 -->
      <tabs
        :todos="todos"
        :active="active"
        @toggleFilter="toggleFilter"
        @clearAllCompleted="clearAllCompleted"
      ></tabs>
    </fieldset>
  </div>
</template>

<script>
import TodoItem from "./TodoItem";
import Tabs from "./Tabs";

export default {
  components: {
    TodoItem,
    Tabs
  },
  data() {
    return {
      newTodoText: "",
      todos: [],
      nextTodoId: 1,
      active: "全部"
    };
  },
  methods: {
    addNewTodo() {
      if (this.newTodoText) {
        this.todos.push({
          id: this.nextTodoId++,
          title: this.newTodoText,
          isDone: false,
          isEdit: false
        });
        this.newTodoText = "";
      }
    },
    changeText(e) {
      this.newTodoText = e.target.value.trim();
    },
    changeTodos(index) {
      this.todos.splice(index, 1);
    },
    toggleFilter(state) {
      this.active = state;
    },
    clearAllCompleted() {
      this.todos = this.todos.filter(todo => !todo.isDone);
    },
    //完成全选按钮
    allSelected() {
      if (
        this.todos.length ==
        this.todos.filter(todo => todo.isDone == true).length
      ) {
        this.todos.map(todo => {
          todo.isDone = false;
        });
      } else {
        this.todos.map(todo => {
          todo.isDone = true;
        });
      }
    }
  },
  computed: {
    filterTodo() {
      if (this.active === "全部") {
        return this.todos;
      }
      return this.todos.filter(todo =>
        this.active === "已完成" ? todo.isDone : !todo.isDone
      );
    }
  }
};
</script>

<style scoped>
.all-selected {
  display: inline-block;
  width: 40px;
  line-height: 20px;
  cursor: pointer;
  color: red;
  margin-right: 30px;
}
form {
  width: 600px;
  margin: 0 auto;
}
.import-title {
  width: 300px;
  height: 30px;
  padding-left: 15px;
  border-radius: 5px;
  border: 1px solid grey;
  outline: none;
}
.submit-title {
  margin-left: 30px;
  border-style: none;
  background-color: transparent;
  color: red;
  cursor: pointer;
}
</style>