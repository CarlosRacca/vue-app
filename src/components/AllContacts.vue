<template>
    <div id="app">
        <h1>{{ msg }}</h1>
    </div>
</template>

<script>
export default {
    name: 'AllContacts',
    props: {
        msg: String
    }
    
}
</script>

<style scoped>
    #app {
        background-color: rgb(119, 119, 154);
    }
</style>