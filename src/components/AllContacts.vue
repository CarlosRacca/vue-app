<template>
    <div id="app">
        <h1>{{ msg }}</h1>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'AllContacts',
    props: {
        msg: String
    },
    data() {
            return {
                api: []
                
            }
        },
    async mounted () {
        this.api = await axios.get('https://api.coloredstrategies.com/contacts')
        
        
    },
    watch: {
        api: function (){

            this.api.data.data.forEach(e => {
                console.log('contact:',e.id , e.title)
            });

        }
    }
    
}
</script>

<style scoped>
    #app {
        background-color: rgb(119, 119, 154);
    }
</style>