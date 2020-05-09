<template>
    <footer class="footer">
        <span class="todo-count">
            <strong>{{todoNum}}</strong>
            <span v-show="todoNum<=1"> item left</span>
            <span v-show="todoNum>1"> items left</span>
        </span>
        <ul class="filters">
            <li><a href="#/all" :class="{selected : this.$parent.view==='all'}" @click="changeView('all')">All</a></li>
            <li><a href="#/active" :class="{selected : this.$parent.view==='active'}" @click="changeView('active')">Active</a></li>
            <li><a href="#/completed" :class="{selected : this.$parent.view==='completed'}" @click="changeView('completed')">Completed</a></li>
        </ul>
        <button class="clear-completed" @click="clearCompleted">Clear completed</button>
    </footer>
</template>

<script>
    export default {
        name: "Footer",
        methods: {
            changeView(filterView){
                return this.$parent.view = filterView;
            },
            clearCompleted(){
                this.$parent.todoDatas = this.$parent.todoDatas.filter(todo=>!todo.hasCompleted);
            }
        },
        computed: {
            todoNum(){
                return this.$parent.todoDatas.filter(todo=>{
                    return !(todo.hasCompleted);
                }).length;
            }
        }
    }
</script>

<style scoped>

</style>