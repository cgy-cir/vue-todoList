<template>
  <div class="todo-item">
    <input class="todo-checkbox" type="checkbox" v-model="todo.state" />
    <span
      class="todo-title"
      :class="{active:todo.state}"
      v-if="!todo.isEdit"
      v-text="todo.title"
      @click="todo.isEdit = !todo.isEdit"
    ></span>
    <!-- 可修改 -->
    <input
      :class="{active:todo.state}"
      class="edit-title"
      v-else
      type="text"
      v-model="todo.title"
      @blur="todo.isEdit = !todo.isEdit"
      @keyup.enter="todo.isEdit = !todo.isEdit"
      :disabled="todo.state"
    />

    <button class="remove-title" v-show="todo.state" @click="$emit('remove')">删除</button>
  </div>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true
    }
  },
  data() {
    return {};
  }
};
</script>

<style scoped>
.todo-item {
  position: relative;
  left: 72px;
  width: 600px;
  margin: 0 auto;
}
.active {
  text-decoration: line-through;
  background-color: white;
  color: gainsboro;
}
.todo-title {
  text-align: left;
  line-height: 30px;
  display: inline-block;
  /* border-bottom: 1px solid black;
    border-top: 1px solid transparent; */
  width: 300px;
  height: 30px;
  padding-left: 15px;
  margin-top: 10px;
}
.edit-title {
  width: 300px;
  height: 30px;
  padding: 0 0 0 15px;
  border-style: none;
  margin-top: 10px;
  /* border-bottom: 1px solid black;
    border-top: 1px solid transparent; */
}
.todo-checkbox {
  position: absolute;
  top: 19px;
  left: -60px;
}
.remove-title {
  margin-left: 26px;
}
</style>