<template>
    <div id="app" align="justify">

        <!--    first page-->


        <img alt="Vue logo" src="../assets/logo.png">
<!--        <HelloWorld msg="Welcome to Your Vue.js App"/>-->

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

        </ul>

    </div>

</template>

<script>
    export default {
        name: "page2",
        data() {
            return {
                newHuy: "",
                pressed_button: 0,
            }
        },
        props:{
            items: Array
        },
        methods:{
            // удаление элемента на перво странице
            del(index){
                this.$delete(this.items,index)
            },
            page1(){
                this.page = true;
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
            addHuy(){
                this.items.push({done:false, message: this.newHuy }),
                    this.newHuy=""
            },
        }
    }

</script>

<style>

</style>