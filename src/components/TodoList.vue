<template>
    <div class="container">
        <div class="wrapper">
            <input type=text placeholder="Your todos" v-model="newTodo"
            @keyup.enter="addTodo">
        </div>
        <draggable tag="div" v-model="todos" @start='drag=true' @end='drag=false' item-key="todos[index]">
            <div v-for="(todo,index) in todosFiltered" :key="index" class="todo-item">
                <div class="todo-p">
                    <label class="custom-checkbox">
                        <input type="checkbox" v-model="todo.completed">
                        <span></span>
                    </label>
                        <p :class="{completed: todo.completed}">{{ todo.title }}</p>
                </div>
                <button class="x" @click="removeTodo(index)">x</button>
            </div>
        </draggable>
        
        <footer>
            <div id="remaining">
                <p>{{ remaining }} items left</p>
            </div>
            <div id="clear">
                <p @click="completedClear">Clear Completed</p>
            </div>
        </footer>
         <div class="filter" id="filter">
            <p :class="{active: filter=== 'all'}" @click="filter = 'all'">All</p>
            <p :class="{active: filter=== 'active'}" @click="filter = 'active'">Active</p>
            <p :class="{active: filter=== 'allCompleted'}" @click="filter='allCompleted'">Completed</p>
        </div>
        <div class="lastP">
            <p>Drag and drop to reorder list</p>
        </div>
    </div>
</template>

<script>
import { VueDraggableNext } from 'vue-draggable-next';
export default{
    props: ['mode'],
    components:{
      draggable: VueDraggableNext,
    },
    data(){
        return{
            newTodo:'',
            nextId: 3,
            filter: 'all',
            todos:[
                {
                    'id':1,
                    'title': 'Cleaning',
                    'completed': false,
                },
                 {
                    'id':2,
                    'title': 'Jogging',
                    'completed': false,
                }
            ]
        }
    },
    methods:{
        addTodo(){
            if(this.newTodo.trim().length === 0){
                return;
            }
            this.todos.push({
                id: this.nextId,
                title: this.newTodo,
                completed: false,
            });
            this.newTodo ='',
            this.nextId ++;
        },
        removeTodo(index){
            this.todos.splice(index, 1);
        },
        completedClear(){
            this.todos = this.todos.filter(todo =>!todo.completed);
        }
    },
    computed:{
        remaining(){
            return this.todos.filter(todo => !todo.completed).length;
        },
        todosFiltered(){
            if(this.filter === 'all' ){
                return this.todos;
            }else if(this.filter === 'active'){
                return this.todos.filter(todo => !todo.completed);
            }else if (this.filter === 'allCompleted'){
                return this.todos.filter(todo => todo.completed);
            }
            return this.todo;
        }
    }
}
</script>

<style scoped>

.container{
    margin: 0 auto;
    transform: translateY(-140px)
}
.todo-item{
    background: #25273C;
    padding: 0.5rem;
    border-bottom: 1px solid #777A92;
    width: 80%;
    margin:0 auto;
    display: flex;
    justify-content: space-between;
    transition: background 0.3s ease-in-out;
    animation: fadeIn ease 0.7s;
}
@keyframes fadeIn{
    from{opacity: 0;}
    to{opacity: 1;}
}
.todo-p{
    display: flex;
    justify-content: flex-start;
    align-items: center;
}
.completed{
    text-decoration: line-through;
    opacity: .2;
}
/*Checkbox styling */
.custom-checkbox input{
    display: none;
}
.custom-checkbox span{
   width: 25px;
   height: 25px;
   background-color: transparent;
   border: 1px solid#CACDE8;
   border-radius: 50%;
   outline: none;
   margin: 0.5rem 1rem;
   cursor: pointer;
   display: flex;
   justify-content: center;
   align-items: center;
}
.custom-checkbox input:checked + span{
  background: linear-gradient(#57DDFF, #C058F3); 
  border:none;
}
.custom-checkbox input:checked + span:before {
   content: "✔";
}
/*Checkbox styling end */
.wrapper{
    margin: 0 auto;
    width: 80%;
}
input{
  display: flex;
  align-items: center;
  background-color: #25273C;
  border-radius: 5px;
  color: #ccc;
  outline: none;
  width: 100%;
  padding: 25px 22px 20px;
  border: none;
  font-size: 18px;
  margin: 1.5rem auto;
  text-align: center;
}
.x{
    font-size: 2rem;
    background: transparent;
    border:none;
    color: #393A4C;
    float: right;
    cursor: pointer;
}
.x:focus{
    outline:none;
}


/* footer styles =>  */
footer{
    display: flex;
    justify-content: space-between;
    background: #25273C;
    padding: 0.5rem;
    width: 80%;
    margin:0 auto;
    border-bottom-left-radius: 5px;
    border-bottom-right-radius: 5px;
}
#filter{
    display: flex;
    justify-content:center;
    text-align: center;
    transform: translateY(25px);
    margin: 0 auto;
    background: #25273C;
    width: 80%;
    border-radius: 5px;
}
#filter p{
    padding: 0.6rem 0.5rem;
    cursor: pointer;
}
.all, .allCompleted, .active{
    color: #3A7BFD;
    opacity: 1;
}
footer p{
    opacity: .2;
}
#remaining p{
    margin-left: 1rem;
}
#clear p{
    margin-right: 0.8rem;
    cursor: pointer;
}
.lastP{
    display: flex;
    justify-content: center;
    margin: 5rem auto;
    opacity: .2;
}
/* MEDIA QUERIES */

@media screen and (min-width: 880px){
    .todo-item{
        width: 60%;
    }
    .wrapper{
        width: 60%;
    }
    footer{
        width: 60%;
    }
    #filter{
        background: transparent;
        width: 30%;
        padding:0;
    }
    .light #filter{
        background: transparent !important;
    }
    #filter p{
        transform: translateY(-96px);
    }
    .lastP{
        margin: 0.3rem auto;
    }
}
/* Light Mode */
.light input{
    background: #FAFAFA;
    color: #161722;
}
.light .todo-item{
    background: #FAFAFA;
    color: #161722;
}
.light footer{
    background: #FAFAFA;
    color: #9394A5;
}
.light p{
    opacity: 1;
}
.light #filter{
    color: #9394A5;
    background: #FAFAFA;
}
</style>