<template>
  <div class="tabs">
    <span class="unfinish-item">未完成数据: {{unfinishItem}}</span>
    <span
      v-for="(state,index) in states"
      :key="index"
      @click="$emit('toggleFilter',state);changeActive(state)"
      class="abc"
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
      states: ["全部", "未完成", "已完成"]
    };
  },
  mounted() {
    let all = document.getElementsByClassName("abc")[0];
    all.classList.add("active");
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
    changeActive(state) {
      let all = document.getElementsByClassName("abc")[0];
      let unfinish = document.getElementsByClassName("abc")[1];
      let finished = document.getElementsByClassName("abc")[2];
      all.className = "";
      unfinish.className = "";
      finished.className = "";
      if (state == "全部") {
        all.classList.add("active");
      } else if (state == "未完成") {
        unfinish.classList.add("active");
      } else if (state == "已完成") {
        finished.classList.add("active");
      }
      all.classList.add("abc");
      unfinish.classList.add("abc");
      finished.classList.add("abc");
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