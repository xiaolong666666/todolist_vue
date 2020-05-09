<template>
    <li :class="{completed:todo.hasCompleted,editing:edit===todo}">
        <div class="view">
            <input type="checkbox" class="toggle" v-model="todo.hasCompleted">
            <label @dblclick="editTodo(todo)">{{todo.value}}</label>
            <button class="destroy" @click="deleteTodo(todo)"></button>
        </div>
        <input type="text" class="edit" v-focus v-model="edit.value"
            @keyup.enter="doneTodo" @blur="doneTodo" @keyup.esc="escTodo(index)"
        >
    </li>
</template>

<script>
    export default {
        name: 'Item',
        props: ['todo','index'],
        data(){
            return {
                edit: "",
                value: "",
            }
        },
        methods: {
            deleteTodo(todo){
                this.$parent.todoDatas = this.$parent.todoDatas.filter(value=>{
                    return !(value.id===todo.id);
                })
            },
            editTodo(todo){
                this.edit = todo;
                this.value = todo.value;
            },
            doneTodo(){
                this.edit = "";
            },
            escTodo(index){
                this.$parent.todoDatas[index].value = this.value;
                this.edit = "";
            }
        },
        directives: {
            focus(el){
                el.focus();
            }
        }
    }
</script>

<style scoped>

</style>