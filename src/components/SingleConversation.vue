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
        
        <h1 class="chatTop"  v-else>
            Choose one chat
        </h1>
        
        
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

    mounted () {
        console.log(this.chat)
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

            console.log(this.chat)
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

    .divIf {
        width: 100%;
    }

    .chatTop {
        background-color: green;
        width: 100%;
        height: 100px;
        margin-top: 0px;
        display: flex;
        /* flex-direction: column; */
        justify-content: flex-start;
        align-items: center;
        padding-left: 100px;
    }

    .chatName {
        color: wheat;
        padding-right: 100px;
    }

    .lastSeen{
        font-size: 20px;
        text-decoration: none;
    }
    
    .myChat{
        display: flex;
        background-color: white;
        justify-content: space-between;
        padding-left: 20px;
        padding-right: 20px;
        margin-left: 200px;
    }

    .otherChat{
        display: flex;
        background-color: sienna;
        justify-content: space-between;
        padding-left: 20px;
        padding-right: 20px;
        margin-right: 200px;
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
        font-size: 25px;
        padding-left: 50px;
    }::placeholder{
        display: flex;
        margin: 10px;
        padding: 10px;
    }

    .buttonSend{
        width: 75px;
        background-color: rgb(79, 118, 191);
        border: none;
        border-radius: 100%;
        font-size: 25px;
        margin-right: 5px;
        /* text-decoration: bold; */
        color: cornsilk;
    }
</style>