<template>
    <div id="app">
        <h1>{{ msg }}</h1>
    </div>
</template>

<script>
export default {
    name: 'TextBar',
    props: {
        msg: String
    }
    
}
</script>

<style scoped>
    #app {
        background-color: rgb(87, 121, 93);
    }
</style>