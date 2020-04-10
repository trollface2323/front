<template>
    <div>
        <div class="background">
        <div class="date">
            {{data}}
        </div>

        <div class="text_area">
        <p><br>
            <input v-model="newHuy" type="text" align="center" v-on:keyup.enter="addHuy" placeholder="Enter a task"> &emsp;
            <input type="submit" value="Add Task" @click="addHuy" id="add_button">
        </p>
        </div>
        <div align="left">
        <ul>
            <li v-for="(item, index) in items" :key="item.message">
                <input type="checkbox" v-model="item.done">

                <span v-if="item.done"><s>{{index+1}} {{item.message}}</s></span>
                <span v-else>{{index+1}}: {{item.message}}</span> &emsp;
                <input type="submit" value="delete" @click="del(index)" align="right">
            </li>
            <p></p>
            <input type="submit" value="check all" @click="check_all"><br>

        </ul>
        </div>
        </div>
    </div>

</template>

<script>
    export default {
        name: "page2",
        data() {
            return {
                newHuy: "",
                pressed_button: 0,
                data: new Date(),

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
    #add_button {
        background: lightblue;
        border-radius: 5px;

    }
    .background{
        background-color: gray;
        width: 800px;
        height: 350px;
        padding-left: 100px;
        padding-top: 50px;
        margin-left: 150px;
        border-radius: 5px;
    }
    .text_area{
        border-bottom: 10px green;
        margin-left: 22px;
    }
    .date{
        margin-left: 22px;
    }
</style>