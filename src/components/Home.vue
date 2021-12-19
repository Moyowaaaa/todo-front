<template>
    <div>


        <div class="navbar">
            <h1>Todos</h1>
        </div>


        <div class="form">
            <input type="text" placeholder="Add something..............." v-model="Title">
            <br>
            <button @click="addTodo"><img src="../assets/check-mark.svg" /></button>
        </div>


       
        <div class="todo" v-for="todo in todos" :key="todo._id" :id="todo._id" :todo="todo"
        >

        <div class="L">
                <p>{{ todo.Title }}</p>
        </div>
            

                 <div class="R">
                <button v-on:click="deleteTodo(todo._id)"><img src="../assets/trash.svg" /></button>
            </div>
        </div>

        <!--------------
        <div class="test">
            <div class="L"></div>


            <div class="R">
                <button v-on:click="deleteTodo(todo._id)"><img src="../assets/trash.svg" /></button>
            </div>
        </div>----------->
    </div>
</template>


<script>
import axios from 'axios'

export default {
    name: 'Home',
    data() {
        return{
            todos: [],
            id:'',
            Title:''
        }
    },
    async created() {
        try{
            const response = await axios.get('http://localhost:5000/')
            this.todos = response.data
        }
        catch(err) {
            console.log(err)
        }
    },
    methods: {
        async addTodo(){
            const response = await axios.post('http://localhost:5000/', {
                Title: this.Title
            })
            this.todos = response.data
            location.reload()
        },
        async deleteTodo(id) {
            const response = await axios.delete('http://localhost:5000/' + id)
            this.todos = response.data
             location.reload()
        }
    }
    
}
</script>
<style scoped>
.navbar{
    width:100%;
    text-align:center


}
.form{
    margin-left:25%;
    width:55%
}
input[type=text] {

    width:90%;
    height:30px
}
.but{
    color:red;
}
button{
    background:royalblue;
    border:none;
    color: white;
    height:30px;
    margin-top:3%;
    margin-left:45%;
    width:auto;
}
.form button{
    background: none;;
     background: royalblue;
    margin-left:85%;
    border-radius: 10px;
}
.todo{
    margin-left:25%;
    height:auto;
    width:50%;
    background:royalblue;
    color: white;
    display: flex;
    margin-top:2%;
}
.L p{
    padding-left:5%
}
.todo .L{
    width:90%;
}
.R {
    width:auto;
    background:none;
    color:red;
    padding:1%
    
}
button img{

}
@media screen and (max-width: 480px) {
    .navbar{
        padding-top:5%;
    }
    .form{
        width:80%;
        margin-left:10%;
    }
    input[type=text]{
        width:95%
    }
    .form button{
        width:auto;
        margin-top:10%;
        margin-left:85%;
        height:30px
    }
    .todo{
        margin-left:10%;
        width:80%;
        margin-top:5%;
    }
    .todo .L{
        width:75%;
    }
    .R{
        margin-top:2%
    }
}
</style>