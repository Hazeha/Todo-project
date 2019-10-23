
<template>
    <div class="is-centered columns">
    <form class="box column is-fullwidth is-four-fifths-tablet is-three-fifths-desktop" @submit.prevent="createTodo()">
        <header>
            <h1 class="subtitle">Create Todo</h1>
        </header>

        <div class="field">
            <label class="label">Subject</label>
            <input class="newTodo input" type="text" placeholder="What needs to be done?" v-model="todo.subject">
        </div>

        <div class="field">
            <label class="label">Description</label>
            <div class="control">
                <textarea class="textarea" placeholder="Enter Description of problem" v-model="todo.description"></textarea>
            </div>
        </div>

        <div class="field">
            <label class="label">Category</label>
            <div class="control">
                <div class="select is-fullwidth">
                    <select v-model="todo.category">
                        <option>Cleaning</option>
                        <option>Tech</option>
                        <option>Serving</option>
                        <option>Unauthorized</option>
                    </select>
                </div>
            </div>
        </div>

        <div class="field">
            <label class="label">Area</label>
            <div class="control">
                <div class="select is-fullwidth">
                    <select v-model="todo.area">
                        <option>Hall 1</option>
                        <option>Hall 2</option>
                        <option>Restaurant</option>
                        <option>Room 132</option>
                        <option>Room 133</option>
                        <option>Conference Room 1</option>
                        <option>Conference Room 2</option>
                    </select>
                </div>
            </div>
        </div>

        <div class="field">
            <label class="label">Importance</label>
            <div class="control">
                <div class="select is-fullwidth" >
                    <select v-model="todo.importance">
                        <option>Low</option>
                        <option>Medium</option>
                        <option>High</option>
                        <option>Asap</option>
                    </select>
                </div>
            </div>
        </div>

        <div class="field">
            <div class="control">
                <button type="submit" class="button is-link is-centered">Submit</button>
            </div>
        </div>

    </form>
    </div>
</template>

<script>
    import {db} from "@/firebaseconfig"
    export default {
        name: "todoForm",
        data: () =>{
            return{
                todo:{
                    subject: "",
                    description: "",
                    category: "",
                    area: "",
                    importance: ""
                }
            }
        },
        methods: {
            async createTodo(){
                await db.collection("todos").add({
                    subject: this.todo.subject,
                    description: this.todo.description,
                    category: this.todo.category,
                    area: this.todo.area,
                    importance: this.todo.importance,
                    user: "testuser",
                    finished: false,
                    date: new Date()
                })

                    this.todo.subject = "",
                    this.todo.description = "",
                    this.todo.category = "",
                    this.todo.area = "",
                    this.todo.importance = ""
            }
        }
    }



</script>

<style scoped>
    form{
        background: #fff;
        margin: 30px 15px 40px 25px;

        position: relative;
        box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.2), 0 25px 50px 0 rgba(0, 0, 0, 0.1);

    }
    .button{
        width: 150px;
        margin-left: calc(50% - 75px);
    }
</style>