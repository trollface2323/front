<template>
  <div>
  <div v-if="page" id="app" align="justify">

<!--    first page-->


    <img alt="Vue logo" src="./assets/logo.png">
        <HelloWorld msg="Welcome to Your Vue.js App"/>

    <a><br>
      <span> <b>Список вещей</b></span><br>
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
      <input type="submit" value="check all" @click="check_all"><br>

      <input type="submit" value="page 1" @click="page1"> &emsp;
      <input type="submit" value="page 2" @click="page2">



    </ul>

  </div>

<!--     second page-->
  <div v-if="!page" align="center">
      <img alt="Vue logo" src="./assets/logo.png"> <br>
      <span><b> Список команды </b></span><br>
      <ul>
        <input v-model="newHuy2" type="text" align="center" v-on:keyup.enter="addHuy2"> &emsp;

        <li v-for="(teams, index) in teams" :key="teams.name">
          <input type="checkbox" v-model="teams.done">

          <span v-if="teams.done"><s>{{index+1}}: {{teams.name}}</s></span>
          <span v-else>{{index+1}}: {{teams.name}}</span> &emsp;
          <input type="submit" value="delete" @click="del2(index)">
        </li>
        <p></p>
        <input type="submit" value="check all" @click="check_all2">

      </ul>

    <input type="submit" value="page 1" @click="page1"> &emsp;
    <input type="submit" value="page 2" @click="page2">
    </div>
  </div>
</template>

<script>
  import HelloWorld from './components/HelloWorld.vue'

  export default {
    name: 'App',
    components: {
      HelloWorld
    },
    data(){
      return{
        newHuy:"",
        newHuy2:"",
        page:true, // выбор отображаемой страницы

        //name2:"punkt 1",
        // name2:"punkt 2",
        items:[
          {name:"name",done:false, id:2, message: 'message'},
          {name:"name2",done:false, id:1, message:'message2'}
        ],
        teams:[
          {name:"kalash",done:false, id:2, message: 'her'},
          {name:"Lyoha",done:false, id:1, message:'her2'}
        ],

        pressed_button: 0,
        pressed_button1: 0,
        a:0,
        b: 0

      }
    },
    methods:{
      // удаление элемента на перво странице
      del(index){
          this.$delete(this.items,index)
      },
      // удаление элемента на второй странице
      del2(index){
          this.$delete(this.teams,index)
      },
      page1(){
        this.page = true;
      },
      page2(){
        this.page = false;
      },
      check_all(){
        for (let i = 0; i < this.items.length; i++){
          if (this.items[i].done){
            this.a = 1
          } else{
            this.pressed_button = 1;
          }
        }
        this.items.forEach((v) => {
          if (this.pressed_button == 0){
            v.done = false; // расчеркивает должно
          } else {
            v.done = true;
          }
        });
        this.pressed_button = 0;
      },
      check_all2(){
        for (let i = 0; i < this.teams.length; i++){
          if (this.teams[i].done){
            this.a = 1
          } else{
            this.pressed_button1 = 1;
          }
        }
        this.teams.forEach((v) => {
          if (this.pressed_button1 == 0){
            v.done = false; // расчеркивает должно
          } else {
            v.done = true;
          }
        });
        this.pressed_button1 = 0;
      },
      huy({target}){
        console.log(target.value)
      },
      addHuy(){
        this.items.push({done:false, message: this.newHuy }),
                this.newHuy=""
      },
      addHuy2(){
        this.teams.push({done:false, name: this.newHuy2 }),
                this.newHuy2=""
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
