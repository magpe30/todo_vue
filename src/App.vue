<template>
  <div class="app" :class="(mode === 'light') ? 'light' : 'dark'">
    <the-header :mode='mode' @toggle="toggle"></the-header>
    <todo-list :mode='mode'/>
  </div>  
</template>

<script>
import TheHeader from './components/TheHeader.vue';
import TodoList from './components/TodoList.vue';

export default {
  name: 'App',
  components: {
    TheHeader,
    TodoList
  },
  data(){
    return{
      mode: 'light',
    }
  },
  methods:{
    toggle(){
      if(this.mode === "dark"){
        this.mode = "light"
      }else{
        this.mode = "dark"
      }
    },
    
  },
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Josefin+Sans&display=swap');
* {
  box-sizing: border-box;
  font-family: 'Josefin Sans' , sans-serif;
}
body{
  padding:0;
  margin:0;
  min-height: 100%;
}
#app{
  width: 100%;
  min-height: 100vh;
  transition: background 0.3s ease-in-out;
  background-color: #161722;
  font-size: 18px;
}

.dark{
  color: #FFFFFF;
}
.light{
  background-color: #E4E5F1;
  min-height: 100vh;
}
</style>
