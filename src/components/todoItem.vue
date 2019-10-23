<template>

    <div class="is-centered columns is-multiline">

        <div class=" column is-centered is-fullwidth is-four-fifths-tablet is-three-fifths-desktop" v-for="todo in todos"  v-bind:key="todo.id  ">
            <div class="todo-card card" v-bind:class="{ 'completed' : todo.finished != false}">

                <header class="card-header" v-bind:class="{ 'high' : todo.importance == 'High', 'medium' : todo.importance == 'Medium', 'low' : todo.importance == 'Low', 'right-now' : todo.importance == 'Asap'}">
                    <p class="card-header-title">
                        {{todo.subject}}
                    </p>
                    <p class="category">{{todo.category}}</p>
                </header>
                <div class="card-content">

                        <p>{{todo.description}}</p>

                    <p>{{todo.area}}</p>

                        <hr>
                        <time :datetime="todo.date">{{ todo.date.toDate()}}</time>


                </div>
                <footer class="card-footer">
                    <a href="#" class="card-footer-item">Finished</a>
                    <a href="#" class="card-footer-item">Edit</a>
                </footer>
            </div>
        </div>
    </div>
</template>
<!--TODO add class completed if todo is completed=true-->
<script>
    import {db} from "@/firebaseconfig"
    export default {
        name: "todoItem",

        data() {
            return {
                todos: []
            }
        },
        methods: {
            async getTodos(){
                let data = []
                await db.collection("todos").get().then((querySnapshot) => {
                    querySnapshot.forEach(doc => data.push({
                        id: doc.id,
                        ...doc.data()
                    }))
                })
                this.todos = data
            },
            //TODO infil af completion function

        },
        created() {
            db.collection('todos').onSnapshot(doc => {
                const changes = doc.docChanges()

                changes.forEach(change => {
                    if (change.type === 'added') {
                        this.todos.push({
                            id: change.doc.id,
                            ...change.doc.data()
                        })
                    }

                    if (change.type === "removed") {
                        const doc = this.todos.indexOf(change.doc.id)
                        this.todos.splice(doc, 1)
                    }
                })
            })
        }
    }

</script>

<style scoped>
    .completed{
        background: #a0a0a0;
    }
    .card-content{
        text-align: left;
    }
    .category{
        padding: 12px;
    }
    time{
        float: right;
    }
    .right-now{
        border: red 1px solid;
    }
    .high{
        border: #dc5240 1px solid;
    }
    .medium{
        border: darkgoldenrod 1px solid;
    }
    .low{
        border: greenyellow 1px solid;
    }
    .todo-card{
        background: #fff;
        box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.2), 0 5px 10px 0 rgba(0, 0, 0, 0.1);
        border-radius: 10px;
    }
</style>