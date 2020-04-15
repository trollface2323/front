<template >
  <div class="background_general">
    <div class="background">
      <span class="span_time"> {{date}} </span>

      <span class="span_input">
      <input type="submit" value="Incomplete Tasks" @click="page1" class="input"> &emsp;
      <input type="submit" value="Complete Tasks" @click="page2" class="input">
      </span><br>
<!--      TODO: FGHJKL-->
      <span class="size"> 2 Active Tasks</span>

      <Page v-if="page" :items="items"></Page>
      <Page v-else :items="teams"></Page>
    </div>
      </div>
</template>

<script>
  var moment = require('moment');
  console.log(moment(). format());
  moment.locale('ru');
  // import HelloWorld from './components/HelloWorld.vue'
  import Page from './components/Page.vue'


  export default {
    name: 'App',
    components: {
      // HelloWorld,
      Page
    },
    data(){
      return{
        date: moment().format("dddd, MMM D" ),
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

      }
    },
    methods:{
      // удаление элемента
      del(index){
          this.$delete(this.items,index)
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
/* изменяем шрифт*/
  @import url('https://fonts.googleapis.com/css2?family=Roboto:wght@100&display=swap');

  ul#app>li{

  }

  .background_general {
    background: #61DBFB; /* Цвет фона */
    height: auto;
    width: 100%;
    padding-top: 100px;
    color: white;
  }
  /*изменяем шрифт*/
  div{
    font-family: 'Roboto', sans-serif;
  }
   /*псевдокласс*/

  .hover:hover{
      color:green;
    }
  .span_input{
    float: right;
    margin-right: 70px;
  }
  .background{
    background-color: #393F49;
    width: 800px;
    /*height: 350px;*/
    padding-left: 100px;
    padding-top: 50px;
    margin-left: 150px;
    border-radius: 5px;
    box-shadow: 2px 2px 10px 2px gray;

  }
  .span_time {

  }
  .input{
    background-color: #393F49;
    border: 0;
    outline: none;
    color: white;
  }
  active:active {
    color: red;
  }
  .enable{
    color: #D1D2D4;
  }
  .disable{
    color: #777B81;
  }
  .size{
    font-size: 12px;
    color: #53A4BC;
  }

</style>
  