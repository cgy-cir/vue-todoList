<template>
  <div class="tabs" >
    <span class="unfinish-item">未完成数据{{unfinishItem}}</span>
    <span 
      v-for="(state,index) in states" 
      :key="index"
      @click="$emit('toggleFilter',state)"
      :class="active === state ? '未完成' : ''"
      
    >
      {{state}}
    </span>
    <span 
      class="clear-finish"
      @click="$emit('clearAllCompleted')"
      v-show="show"
    >
      清除已完成
    </span>
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
      states: ['全部','未完成','已完成']
    }
  },
  computed: {
    unfinishItem() {
      return this.todos.filter(todo => !todo.state).length
    },
    show() {
      return this.todos.filter(todo => todo.state).length !== 0
    }
  },
}
</script>


<style scoped>
.tabs{
  width: 600px;
  margin: 20px auto;
}

.active{
  border: 1px solid black;

}
span{
  margin: 0 20px;
}
.clear-finish{
  margin-left: 50px;
}
</style>