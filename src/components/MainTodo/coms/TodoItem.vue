<template>
    <div :class="['todo-item',todo.completed ? 'completed':'']">
        <input type="checkbox" v-model="todo.completed">
        <label>{{todo.content}}</label>
        <button @click="delItem"></button>
    </div>
</template>

<script>
export default {
    name:'TodoItem',
    props:{
        todo:Object
    },
    methods:{
        delItem(){
            this.$emit('del',this.todo.id)
        }
    }
}
</script>

<style scoped>
.todo-item{
    display: flex;
    justify-content:space-between;
    padding: 10px;
    font-size: 24px;
    border-top:1px solid rgba(0,0,0,.1);
}
.todo-item.completed label{
    color: #d9d9d9;
    text-decoration: line-through;
}
.todo-item:hover button::after{
    content: 'x';
    font-size: 24px;
    color:rgb(226, 62, 21);
}
.todo-item label{
    flex: 1;
    transition: color 0.4s;
}
.todo-item input{
    width: 50px;
    height: 30px;
    text-align: center;
    appearance: none;
    border: none;
    outline: none;
}
.todo-item input:after{
    content: url('../../../assets/images/unchecked.svg');
}
.todo-item input:checked::after{
    content: url('../../../assets/images/checked.svg');
}
.todo-item button{
    appearance: none;
    border: none;
    outline: none;
    width: 40px;
    background-color: transparent;
    cursor: pointer;
}

</style>>
