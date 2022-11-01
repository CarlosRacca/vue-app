<template>
    <div id="app">
        <h1>{{ msg }}</h1>
    </div>
</template>

<script>

import axios from 'axios'

export default {
    name: 'AllChats',
    props: {
        msg: String
    },
    data() {
            return {
                api: []
                
            }
        },
    async mounted () {
        this.api = await axios.get('')
        
    },
    
}
</script>

<style scoped>
    #app {
        background-color: rgb(154, 119, 119);
    }
</style>