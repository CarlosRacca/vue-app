<template>
    <div id="app">
        <h1>{{ msg }}</h1>
    </div>
</template>

<script>
export default {
    name: 'SingleConversation',
    props: {
        msg: String
    }
    
}
</script>

<style scoped>
    #app {
        background-color: aqua;
    }
</style>