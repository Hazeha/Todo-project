<template>
    <section class="hero is-fullwidth">
            <div class="container">
                    <img class="logo" src="@/assets/logo.png" alt="Business Todo">
                <h1 class="title">
                    Todo-it Business
                </h1>
            </div>
    </section>
</template>
<style>
    .logo{
        height: 100px;
    }
    h1.title{
        margin-bottom: 0.2rem!important;
    }
    .navLink{
        margin: 0 25px;
        color: #00B7FF;
        font-size: 16pt;
    }
</style>

<script>
    export default {
        name: 'Hero'
    }
</script>
