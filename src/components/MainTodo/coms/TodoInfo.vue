<template>
<div class="todo-info">
    <span class="total">还有{{total}}件事未完成</span>
    <div class="tabs">
    <a v-for="(item,index) of states" :key="index" :class="item==state?'actived':''" @click="toggleState(item)">{{item}}</a>

    </div>
    <button class="clear" @click="clearCompleted"> clear completed</button>
</div>

</template>

<script>
export default {
    name:'TodoInfo',
    props:{
        total:Number
    },
    data(){
        return{
            states:['全部事项','正在进行','已完成'],
            state:'全部事项'
        }
    },
    methods:{
        toggleState(state){
            this.state=state
            this.$emit('toggleState',state)
        },
        clearCompleted(){
            this.$emit('clearCompleted')
        }
    }
}
</script>

<style scoped>
.todo-info{
    display: flex;
    justify-content:space-between;
    font-weight: 400;
    padding: 5px 10px;
    line-height: 30px;
    border-top:1px solid rgba(0,0,0,.1) ;
}

.total{
    color: skyblue;
}
.tabs{
    display: flex;
    justify-content: space-between;
    width: 200px;
}
.tabs a{
    border: 1px solid skyblue;  
    border-radius: 5px;
    padding: 0 5px;
}
.tabs a.actived{
    background-color: skyblue;
    color: snow;
}
.clear{
    padding: 0 5px;
    background-color: green;
    border-radius: 5px;
    color: white;
    appearance: none;
    border: none;
    outline: none;
}
</style>