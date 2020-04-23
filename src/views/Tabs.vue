<template>
  <div class="tabs">
    <span class="unfinish-item">未完成数据: {{unfinishItem}}</span>
    <span
      v-for="(state,index) in states"
      :key="index"
      @click="$emit('toggleFilter',state);changeActive(index)"
      :class="{active:index === activeIndex}"
    >{{state}}</span>
    <span class="clear-finish" @click="$emit('clearAllCompleted')" v-show="show">清除已完成</span>
  </div>
</template>


<script>
export default {
  props: {
    todos: {
      type: Array,
      required: true
    },
    active: {
      type: String
    }
  },
  data() {
    return {
      states: ["全部", "未完成", "已完成"],
      activeIndex: 0
    };
  },
  computed: {
    unfinishItem() {
      return this.todos.filter(todo => todo.isDone === false).length;
    },
    show() {
      return this.todos.filter(todo => todo.isDone).length !== 0;
    }
  },
  methods: {
    changeActive(index) {
      this.activeIndex = index;
    }
  }
};
</script>


<style scoped>
.tabs {
  width: 600px;
  margin: 20px auto;
}

.active {
  border: 1px solid black;
}
span {
  cursor: pointer;
  margin: 20px;
  padding: 5px;
  border-radius: 5px;
}
.clear-finish {
  margin-left: 50px;
}
</style>