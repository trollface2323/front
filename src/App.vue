<template>
  <div id="app" align="justify">
    <img alt="Vue logo" src="./assets/logo.png">
    <!--    <HelloWorld msg="Welcome to Your Vue.js App"/>-->
    <a><br>
      <input v-model="newHuy" type="text" align="center" v-on:keyup.enter="addHuy"> &emsp;
      <input type="submit" value="send" @click="addHuy">

    </a>
    <ul>
      <li v-for="(item, index) in items" :key="item.message">
        <input type="checkbox" v-model="item.done">

        <span v-if="item.done"><s>{{index+1}} {{item.message}}</s></span>
        <span v-else>{{index+1}}: {{item.message}}</span> &emsp;
        <input type="submit" value="delete" @click="del(index)">
      </li>
      <p></p>
      <input type="submit" value="check all" @click="check_all">



    </ul>
  </div>
</template>

<script>
  // import HelloWorld from './components/HelloWorld.vue'

  export default {
    name: 'App',
    components: {
      // HelloWorld
    },
    data(){
      return{
        newHuy:"",

        //name2:"punkt 1",
        // name2:"punkt 2",
        items:[
          {name:"huy",done:false, id:2, message: 'her'},
          {name:"huy2",done:false, id:1, message:'her2'}
        ],
        pressed_button: 0

      }
    },
    methods:{
      del(index){
          this.$delete(this.items,index)
      },
      check_all(){
        this.items.forEach((v) => {
          if (this.pressed_button == 0){
            v.done = true;
            } else {
            v.done = false;
          }
        });
        if (this.pressed_button == 0){
          this.pressed_button = 1;
        } else {
          this.pressed_button = 0;
        }
      },
      huy({target}){
        console.log(target.value)
      },
      addHuy(){
        this.items.push({done:false, message: this.newHuy}),
                this.newHuy=""
      },
    }
  }
</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>
