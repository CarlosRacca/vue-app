<template>
    <div id="app">
        <h1>{{ msg }}</h1>
        <form action="">
            <input type="text" placeholder="Say something">
            <button>Send</button>
        </form>
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