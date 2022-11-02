<template>
    <div id="app">
        <h1>{{ msg }}</h1>
        <div v-if="this.existingChat">
            <h1>
                {{this.chat.name}}
            </h1>
            <p v-for="element in this.chat.messages" :key="element.id">
                {{element.sender}} -- {{element.text}} -- {{element.time}}
            </p>
            
        </div>
        <div v-if="this.newChat">
            <h2>Empeza un nuevo chat</h2>
        </div>
        <form action="">
            <input type="text" placeholder="Say something">
            <button>Send</button>
        </form>
    </div>
</template>

<script>
export default {
    name: 'SingleConversation',
    props: {
        msg: String,
        chat: Object
    },

    data () {
        return {
            newChat: false,
            existingChat: false
        }
    },

    watch: {
        chat: function (){
            console.log('1',this.chat)
            if(this.chat){
                this.existingChat = true
                this.newChat = false
            }
            else{
                this.newChat = true
                this.existingChat = false
            }
        }
    }
    
}
</script>

<style scoped>
    #app {
        background-color: aqua;
    }
</style>