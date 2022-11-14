<template>
    <header class="d-flex m-3">
        <img class="h-100 me-3" src="../assets/img/BB_logo.png" alt="Breaking bad Logo">
        <h1 class="text-center">{{title}}</h1>
    </header>
</template>

<script>
    export default {
        name: 'HeaderComponent',
        props: {
            title: String
        }
    }
</script>

<style lang="scss" scoped>

    header{
        height: 50px;
        
        h1{
            font-weight: 700;
            color: white
        }
    }

</style>