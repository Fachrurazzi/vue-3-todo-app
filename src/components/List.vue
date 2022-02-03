<template>
<div class="col-sm-12">
    <ul class="list-group m-2">
        <li class="list-group-item" v-for="(todo, index) in todos" :key="index">
            <div class="row">
                <div class="col">
                    <span v-if="todo.isDone">
                        <del>{{ todo.activity }}</del>
                    </span>
                    <span v-else>{{ todo.activity }}</span>
                </div>
                <div class="col-auto">
                    <div class="row gx-2">
                        <div class="col">
                            <button @click="done(index)" class="btn btn-info">Done</button>
                            <button @click="deleteTodo(index)" class="btn btn-danger">x</button>
                        </div>
                    </div>
                </div>
            </div>            
        </li>
    </ul>          
</div>  
</template>

<script>
export default {
    props: {
        todos: {
            type: Array,
            default: []
        }
    },
    methods: {
        deleteTodo(index) {
            this.$emit('deleteTodo', index)
        },
        done(index) {
            this.$emit('doneTodo', index)
        }
    }
}
</script>

<style>

</style>