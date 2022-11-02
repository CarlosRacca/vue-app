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
        <form action="" class="formText">
            <input type="text" placeholder="Say something" class="inputText">
            <button class="buttonSend">></button>
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

    .formText {
        width: 100%;
        display: flex;
        height: 70px;
        background-color: rgb(206, 206, 206);
        padding-top:10px;
        padding-bottom: 10px;
        /* padding-left: -25px; */
        border-top: 10px solid black;
        
    }
    .inputText {
        width: 100%;
        border: none;
        background-color: rgb(206, 206, 206);
    }

    .buttonSend{
        width: 75px;
        background-color: cornflowerblue;
        border: none;
        border-radius: 100%;
        font-size: 25px;
        margin-right: 5px;
        /* text-decoration: bold; */
        color: cornsilk;
    }
</style>