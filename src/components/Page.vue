<template>
    <div>
        <div>
        <div class="text_area">
        <p><br>
            <input v-model="newHuy" type="text" align="center" v-on:keyup.enter="addHuy" placeholder="Enter a task"> &emsp;
            <input type="submit" value="Add Task" @click="addHuy" id="add_button">
        </p>
        </div>
        <div align="left">
        <dl>
            <dt v-for="(item, index) in items" :key="item.message" class="list">

                <i class="fas fa-check-circle" style="color: red"></i>

                <input type="checkbox" v-model="item.done" class="checkbox">

                <span v-if="item.done"><s>{{index+1}} {{item.message}}</s></span>
                <span v-else>{{index+1}}: {{item.message}}</span>
                <span style="margin-left: 300px">{{date}}</span>
                <span class="icon"><i class="far fa-trash-alt" ></i></span>
<!--                кнопка удаления-->
<!--                <input type="submit" value="delete" @click="del(index)" class="delete">-->
            </dt>
            <p></p>
<!--            <input type="submit" value="check all" @click="check_all"><br>-->

        </dl>
        </div>
        </div>
    </div>

</template>

<script>
    var moment = require('moment');
    console.log(moment(). format());
    export default {
        name: "page2",
        data() {
            return {
                newHuy: "",
                pressed_button: 0,
                date: moment().fromNow(),
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
            addHuy(){
                this.items.push({done:false, message: this.newHuy }),
                    this.newHuy=""
            },

        }
    }

</script>

<style>
    #add_button {
        background: #61DBFB;
        border-radius: 5px;
    }
    .text_area{
        border-bottom: 2px solid #62686F;

    }
    .delete{
        float:right;
        height: 20px;
        margin-right: 15px;
        background-image: url("");
    }
    .list{
        border-bottom: 2px solid #62686F;
        margin-top: 20px;
        height: 35px;
    }
    .checkbox {
        opacity: 0;
    }
    .icon{
        float: right;
        margin-right: 100px;
    }

</style>