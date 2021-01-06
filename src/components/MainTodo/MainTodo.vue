<template>
<div class="main-todo">
 <input type="text"
   class="add-todo"
   placeholder="今天要做什么?" 
   autofocus
   v-model="content"
   @keyup.enter="addTodo"
    />
 <todo-item v-for="(item,index) of filterDate" :key="index" :todo="item" @del="handledel"></todo-item>
 <todo-info :total="total" @toggleState="handleToggleState" @clearCompleted="handleClear"></todo-info>
</div>
</template>

<script>
import TodoItem from './coms/TodoItem.vue'
import TodoInfo from './coms/TodoInfo.vue'
let id = 0
export default {
    name:'MainTodo',
    data(){
        return{
            todoData:[],
            content:'',
            total:0,
            filter:"全部事项"
        }
    },
    computed:{
        filterDate(){
            switch (this.filter){
                case '全部事项':
                    return  this.todoData
                    break
                case '正在进行':
                    return this.todoData.filter(item => item.completed==false)
                    break
                case '已完成':
                    return this.todoData.filter(item => item.completed==true)
                    break
            }

        }
    },
    methods:{
        addTodo(){
            if (this.content === '') {
                return
            }
            this.todoData.unshift({
                id:id++,
                content:this.content,
                completed:false
            })
            this.content=''
        },
        handledel(id){
            this.todoData.splice(this.todoData.findIndex(item => item.id===id),1)
        },
        handleToggleState(state){
            this.filter = state
        },
        handleClear(){
            this.todoData = this.todoData.filter(item => item.completed==false)
        }
    },
    components:{
        TodoItem,
        TodoInfo
    },
    watch:{
        todoData:{
            deep:true,
            handler(){
              this.total= this.todoData.filter(item => item.completed == false).length
            }
        }
    },
}
</script>

<style scoped>
.main-todo{
    margin: 0 auto;
    width: 600px;
    background-color: #ffffff;
    box-shadow: 0 0 5px #666666;
}
.add-todo{
    font-size: 24px;
    font-weight: inherit;
    font-family: inherit;
    color: inherit;
    border: none;
    outline: none;
    width: 100%;
    padding: 16px 16px 16px 36px;
    box-sizing: border-box;
}
</style>