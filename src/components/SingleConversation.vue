<template>
    <div id="app">
        <div class="divIf" v-if="this.chat.length !== 0">
            <h1 class="chatTop" >
                <a class="chatName">{{this.chat.name}}</a>
                <a class="lastSeen">{{this.chat.date}}</a>
            </h1>
            <div v-if="this.existingChat">
                <h1>
                    
                </h1>
                <div class="conversation" v-for="element in this.chat.messages" :key="element.id">
                    <div v-if="element.sender === 1" class="myChat">
                        <p class="messageName"> Carlos Racca </p>  <p class="messageText">{{element.text}}</p> <p class="messageTime">{{element.time}}  </p> 
                    </div>
                    <div v-else class="otherChat">
                         <p class="messageName">{{this.chat.name}}</p> <p class="messageText">{{element.text}}</p> <p class="messageTime">{{element.time}}</p>
                    </div>
                </div>
                
            </div>
            <div v-else>
                <h2>Start a new chat with {{this.chat.name}}</h2>
            </div>

        </div>
        
        <div class='landing'  v-else>
            <div v-if="this.buttonStart">
                Please choose one chat in the right to start.
            </div>
            <div v-else>
                Welcome to this chat application.

                <button class="buttonOpen" v-on:click="handleStart"> Enter</button>

            </div>
        </div>
        
        
        <form v-if="this.chat.length !== 0" action="submit" class="formText" v-on:submit="handleSend">
            <input type="text" placeholder="Say something" class="inputText" name="text" v-model="text">
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
            existingChat: false,
            text: '',
            modifiedChat: this.chat,
            buttonStart: false
        }
    },

    mounted () {
        
    },

    watch: {
        chat: function (){            
            if(this.chat.messages.length > 0){
                this.existingChat = true
                this.newChat = false
            }
            else{
                this.newChat = true
                this.existingChat = false
            }
        },

        modifiedChat: function () {
            if(this.modifiedChat.messages.length > 0){
                this.existingChat = true
                this.newChat = false
            }
            else{
                this.newChat = true
                this.existingChat = false
            }
        },

    },

    methods: {
        handleStart: function(e){
            e.preventDefault()

            this.buttonStart = true

            this.$emit('showContacts')

        },
        handleSend: function (e){
            this.modifiedChat = this.chat
            e.preventDefault()

            let today = new Date()
            let now = today.toLocaleString().split(' ')[1].split(":")
            let time =  now[0] + ':' + now[1]

            this.modifiedChat.messages.push({
                sender: 1,
                time: time,
                text: this.text
            })

            this.modifiedChat.lastMessageTime = time

            console.log(this.chat)

            this.$emit('chatModified', this.chat)
            
            this.text = ''
        }
    }

    
}
</script>

<style scoped>
    .landing{
        position:relative;
        /* padding:100px;
        /* padding-bottom: 720px; */
        /* padding-right: 0px;
        margin-right: 100px;  */
        
        top:0;
        left:0;
        width: 85vw;
        height: 100vh;
        background:rgb(180, 194, 206);
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 50px;
        display: flex;
        flex-direction: column;
        
        
    }

    .buttonOpen{
        font-family: 'Courier New', Courier, monospace;
        border-radius: 10px;
        margin-top: 100px;
        padding: 40px;
        font-size: 30px;
        background-color: rgb(120, 150, 160);
        color: black;
        box-shadow:  3px 3px  rgb(150, 150, 150);
    }
    #app {
        background-color: rgb(220, 232, 240);
        display: flex;
        flex-direction: column;

        width: 100%;
        align-items: center;
        justify-content: space-between;

    }

    .divIf {
        width: 100%;
    }

    .chatTop {
        background-color: rgb(120, 150, 160);
        border-bottom: 2px solid rgb(30, 54, 73);
        width: 100%;
        height: 100px;
        margin-top: 0px;
        display: flex;
        justify-content: flex-start;
        align-items: center;
        padding-left: 100px;
    }

    .chatName {
        color: rgb(30, 54, 73);
        padding-right: 100px;
    }

    .lastSeen{
        font-size: 20px;
        text-decoration: none;
    }
    
    .myChat{
        border-radius: 10px;
        box-shadow:  3px 3px  rgb(114, 114, 114);
        display: flex;
        background-color: white;
        justify-content: space-between;
        padding-left: 20px;
        padding-right: 20px;
        margin-left: 200px;
        margin-right: 10px;
    }

    .otherChat{
        border-radius: 10px;
        box-shadow:  3px 3px  rgb(114, 114, 114);
        display: flex;
        background-color: rgb(30, 54, 73);
        color: white;
        justify-content: space-between;
        padding-left: 20px;
        padding-right: 20px;
        margin-right: 200px;
        margin-left: 10px;
    }

    .conversation{
        font-size: 30px;
        padding-top: 30px;
        padding-bottom: 30px;
        display: flex;
        flex-direction: column;
    }

    .messageText{
        font-size: 20px;
        
    }

    .messageTime{
        font-size: 20px;
        padding-left: 50px;
    }

    .messageName{
        padding-right: 50px;
        
    }

    .formText {
        width: 100%;
        display: flex;
        height: 70px;
        background-color: rgb(120, 150, 160);
        padding-top:10px;
        padding-bottom: 10px;
        /* padding-left: -25px; */
        border-top: 2px solid rgb(30, 54, 73);
        
    }
    .inputText {
        width: 100%;
        border: none;
        background-color: rgb(120, 150, 160);
        font-size: 25px;
        padding-left: 50px;
    }::placeholder{
        display: flex;
        margin: 10px;
        padding: 10px;
    }

    .buttonSend{
        width: 75px;
        background-color: rgb(30, 54, 73);
        border: none;
        border-radius: 100%;
        font-size: 25px;
        margin-right: 5px;
        /* text-decoration: bold; */
        color: cornsilk;
    }
</style>