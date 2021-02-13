<template>
<div class="main-root">

<transition
leave-active-class="animate__animated animate__zoomOut animate__duration-.3s"
>
<div v-show="show" class="todo-wrapper animate__animated animate__zoomIn animate__duration-.3s">
<div class="input-holder">
    <img @click="show = !show" class="close" :src="buttons.remove" alt="_close-button">
    <h6>{{day}}</h6>
    <input type="text" placeholder="New item..." 
    v-model="newTodo" @keydown.enter="addToList">
    <button class="add-button" @click="addToList()"><img :src="buttons.add" alt="_add-button"></button>
    <button class="clean-button"  @click="clean()"><img :src="buttons.restart" alt="_restart-button"></button>
</div>


<ul class="list-wrapper">
           <li class="todo-item animate__animated animate__backInDown animate__duration-.3s" v-for="todo of todoList" :key="todo">{{ todo }} <button><img @click="removeItem(todo)" :src="buttons.remove" alt="_remove-button"></button> </li>
</ul>

</div>
</transition>
</div>
</template>

<script>
export default {
    name: 'TodoApp',
    data(){
        return {
            show: true,
            buttons: {
                add: require('@/assets/icons/add.png'),
                remove: require('@/assets/icons/remove.png'),
                restart: require('@/assets/icons/restart.png')
            },
            todoList: [],
            newTodo: ''
        }
    },
    methods: {
        addToList(){
            if(this.todoList.includes(this.newTodo.toLowerCase())){
                let res = confirm('You already have this item in your list.Would you like to add anyway?');
                res ? this.todoList.push(this.newTodo.toLowerCase()) : '';
            } else if(this.newTodo.length > 2) {
                this.todoList.push(this.newTodo.toLowerCase());
            } 
            else {
                alert('Please enter at least 3 characters...');
            }
            this.newTodo = "";
        },
        clean(){
            if(this.todoList.length == 0){
                alert('List is empty...');
            } else {
                let res = confirm('Are you sure you want to delete all your todo list?');
                res ? this.todoList = [] : '';
                this.newTodo = '';
            }
        },
        removeItem(item){
            let id = this.todoList.indexOf(item);
            this.todoList.splice(id,1);
        },
        toggleApp(){
            this.show = !this.show;
        }
    },
    computed: {
        day(){
            let d = new Date();
            let day = d.getDay();
            return day == 1 ? 'Monday' : day == 2 ? 'Tuesday' : day == 3 ? 'Wednesday' : day == 4 ? 'Thursday' : day == 5 ? 'Friday' : day == 6 ? 'Sunday' : 'Saturday';
        },
    }
    
}
</script>


<style lang="scss" scoped>
@import '@/assets/style/TodoApp-color.scss';

.todo-wrapper {
    background-color: $todo-background-color;
    color: $todo-day-background;
    width: 300px;
    box-shadow: 10px 10px 30px black;
    border-radius: 12px 12px 8px 8px;
 .input-holder {
     .close {
        width: 10px;
        float: right;
        cursor: pointer;
     }   
     text-align: center;
     background-color: $todo-day-background;
     border-radius: 8px 8px 0 0;
     padding: 10px;
     color: $todo-item-background-color;
     h6 {
         color: $todo-text-color;
         font-size: 20px;
         font-family: georgia;
     }
     input{
            border: none;
            width: 150px;
            height: 20px;
            padding: 5px;
            font-size: 15px;
            color: $todo-day-background;
            font-weight: bold;
            font-family: Arial, Helvetica, sans-serif;
            border-radius: 8px 0 8px 0;
            &:focus {
                border-radius: 0 8px 0 8px;
            }

        }
     
    button {
    background: none;
    border: none;
    transform: translate(10px,5px);
    padding: 2px;
    cursor: pointer;
        img {
        width: 20px;
        background: none;
      
      }
    }
}
    
    .list-wrapper {
        overflow: scroll;
        height:220px;
        margin-top: 10px;
        .todo-item {
            list-style-type: none;
            background-color: $todo-item-background-color;
            padding: 15px;
            margin: 5px 20px 10px -20px;
            border-radius: 7px;
            font-size: 15px;
            word-break: break-all;
            button {
                background: none;
                border: none;
                float: right;
                transform: translate(0,-3px);
                cursor: pointer;
                img {
                    width: 12px;
                } 
            }
        }
    }
}
</style>