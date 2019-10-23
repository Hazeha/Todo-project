<template>
    <div>
        <Hero />
        <div class="is-centered is-vertical is-multiline is-mobile">
        <todoForm/>
        <todoItem/>

        </div>
    </div>
</template>

<script>
// TODO Refresh the new files and import them properly
import Hero from '@/components/Hero.vue'
import todoForm from '@/components/todoForm.vue'
import todoItem from '@/components/todoItem.vue'
import {db} from '@/firebaseconfig'

export default {
    name: 'home',
    components: {
        Hero,
        todoForm,
        todoItem
    }
}
</script>
