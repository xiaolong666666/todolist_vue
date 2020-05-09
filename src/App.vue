<template>
  <section class="todoapp">
    <header class="header">
      <h1>todos</h1>
      <input type="text" class="new-todo" placeholder="What need to be done?" v-model="newTodo" @keyup.enter="addTodo">
    </header>
    <section class="main">
      <input v-if="todoDatas.length===0" type="checkbox" class="toggle-all" id="toggle-all" v-model="isAll" disabled>
      <input v-else type="checkbox" class="toggle-all" id="toggle-all" v-model="isAll">
      <label for="toggle-all"></label>
      <ul class="todo-list">
        <Item v-for="(todo,index) in todoDatasFilter" :key="todo.id" :todo="todo" :index="index"/>
      </ul>
    </section>
    <Footer />
  </section>
</template>

<script>
  import Item from './components/Item'
  import Footer from './components/Footer'
  export default {
    name: "App",
    components: { Item, Footer },
    data(){
      return {
        todoDatas: [],
        newTodo: "",
        view: "all"
      }
    },
    methods: {
      addTodo(){
        if(this.newTodo.trim()==="") return false;
        let todo = {};
        todo.id =+ new Date();
        todo.value = this.newTodo;
        todo.hasCompleted = false;
        this.todoDatas.push(todo);
        this.newTodo = "";
      }
    },
    computed: {
      todoDatasFilter(){
        switch(this.view){
          case "all": return this.todoDatas;
          case "active": return this.todoDatas.filter(todo=>!todo.hasCompleted);
          case "completed": return this.todoDatas.filter(todo=>todo.hasCompleted);
          default: return this.todoDatas;
        }
      },
      isAll: {
        get(){
          return this.$children.todoNum===0;
          // return this.todoDatas.length===this.todoDatas.filter(todo=>todo.hasCompleted).length;
        },
        set(flag){
          this.todoDatas.map(todo=>{todo.hasCompleted=flag;return todo});
        }
      }
    }
  }
</script>

<style scoped>

</style>