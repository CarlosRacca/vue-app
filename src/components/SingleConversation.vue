<template>
    <div id="app">
        <h1 class="chatTop">{{this.chat.name}}</h1>
        <div v-if="this.existingChat">
            <h1>
                
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
        display: flex;
        flex-direction: column;
        /* margin-right: 300px; */
        /* padding-bottom: 100%; */
        width: 100%;
        align-items: center;
        justify-content: space-between;

    }

    .chatTop {
        background-color: green;
        width: 100%;
        height: 100px;
        margin-top: 0px;
    }
</style>