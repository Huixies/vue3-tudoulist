<template>
  <main>
    <div class="container">
      <div class="title1">
        <svg class="icon">
          <use xlink:href="#icon-tudou"></use>
        </svg>
        <h1>TU DOU List</h1>
      </div>
      <TodoAdd 
        :tid='todos.length' 
        @add-todo='addTodo' 
      />
      <TodoFilter 
        :selected='filter' 
        @change-filter="filter = $event" 
      />
      <TodoList :todos='filteredTodos' />
    </div>
  </main>
</template>

<script>
import TodoAdd from './components/TodoAdd';
import TodoFilter from './components/TodoFilter';
import TodoList from './components/TodoList';
import useTodos from '@/composables/useTodos.js';
import useFilteredTodos from '@/composables/useFilteredTodos.js';

export default {
  components:{
    TodoAdd, TodoFilter, TodoList
  },
  setup() {
    const { todos, addTodo } = useTodos();
    const { filter, filteredTodos } = useFilteredTodos(todos);
   
    return { todos, addTodo, filter, filteredTodos }
  },
}
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: Helvetica,'PingFang SC','Microsoft Yahei',sans-serif;
}

/* 整个页面 */
main {
  width: 100vw;
  min-height: 100vh;
  display: grid;
  align-items: center;
  justify-items: center;
  background: rgba(75, 150, 110, 0.609);
}

.title1{
  display: flex;
}

.icon{
  width: 38px;
  height: 38px;
  margin-bottom: 20px;
  color: rgb(75, 150, 110);;
}

.container {
  width: 60%;
  max-width: 400px;
  box-shadow: 0px 0px 24px rgba(0,0,0,0.15);
  border-radius:24px;
  padding:48px 28px; 
  background-color: rgb(247, 247, 247);
}

/* 标题 */
h1 {
  display: inline-block;

  font-size: 28px;
  color: rgb(75, 150, 110);
  margin: 5px 0 0 10px;
}

@media (max-width:700px){
  .container {
    border-radius:0;
    width: 100%;
  }
}
</style>
