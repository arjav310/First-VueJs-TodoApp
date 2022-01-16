<template>
    <div>
        <input v-model="newTodo">
        <button v-on:click="addTodo">ADD</button>
    </div>
</template>

<script>
export default {
    name: 'Input',
    data: {
        todos:[

        ],
        newTodo:''
    },
    methods:{
        addTodo: function(){
            this.todos.push = this.input;
        }
    }
}
</script>