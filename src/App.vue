<template>
  <SingleConversation msg="Conversation" :chat='this.chat'/>
  <div class="buttons">
    <button v-on:click="showContacts" class="buttonClicked" v-if="this.contactsClicked">Contacts</button>
    <button v-on:click="showContacts" class="buttonNotClicked" v-if="!this.contactsClicked">Contacts</button>
    <button v-on:click="showMessages" class="buttonClicked" v-if="this.messagesClicked">Messages</button>  
    <button v-on:click="showMessages" class="buttonNotClicked" v-if="!this.messagesClicked">Messages</button>  
  </div>
  
  <AllContacts classname='Contacts' v-if="viewContacts" msg="Contacts" :contacts="this.apiContactsCleaned" @contactClicked='contactSelected'/>
  <AllChats v-if="viewMessages" msg="Chats" :chats='this.contacts'/>

</template>

<script>
import AllContacts from './components/AllContacts.vue'
import AllChats from './components/AllChats.vue'
import SingleConversation from './components/SingleConversation.vue'
import axios from 'axios'


export default {
  name: 'App',
  components: {
    SingleConversation,
    AllContacts,
    AllChats,

  },
  data () {
    return {
      viewMessages: false,
      viewContacts: true,
      contactsClicked: true,
      messagesClicked: false,
      apiContacts: [],
      apiContactsCleaned: [],
      apiMessages: [],
      apiMessagesCleaned: [],
      contacts: [],
      chat: [],
    }
  },
  async mounted () {
    this.apiContacts = await axios.get("https://api.coloredstrategies.com/contacts")
    this.apiMessages = await axios.get('https://api.coloredstrategies.com/conversations')
  },
  methods: {
    showContacts: function(){
      if(this.viewMessages){
        this.viewMessages = false
      }
      this.viewContacts = true

      this.contactsClicked = true
      this.messagesClicked = false
    },
    showMessages: function(){
      if(this.viewContacts){
        this.viewContacts = false
      }
      this.viewMessages = true

      this.contactsClicked = false
      this.messagesClicked = true
    },

    contactSelected: function (id){

    
      
      this.chat = this.apiMessagesCleaned.filter(el => el.users[1] === id)[0]
      if(this.chat){
        
        this.chat.name = this.apiContactsCleaned.filter(el => el.id === id)[0].title
      }

      
    }
  },
  watch: {
    apiContacts: function(){
      
      this.apiContactsCleaned = this.apiContacts.data.data
    },

    apiMessages: function(){
      
      this.apiMessagesCleaned = this.apiMessages.data.data
    },

    apiMessagesCleaned: function (){

      this.apiContactsCleaned ? this.apiContactsCleaned.forEach(element => {
        this.apiMessagesCleaned.forEach(el => {
          if(el.users.find(id => element.id === id)){
            element.lastMessage = el.lastMessageTime
            this.contacts.push(element)
          }
        })
        
      }) :
      console.log(1)
    }
  }
}
</script>
    
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
  background-size: cover;
  min-height: 100%;
  text-align: center;
  color: #2c3e50;
  /* margin-top: 60px; */
  background-color: tomato;
}

.buttons{
  display: flex;
  justify-content: end;
  height: 100px;
}

.buttonClicked{
  width: 150px;
  font-size: 30px;
  background-color: rgb(73, 36, 175);
}

.buttonNotClicked {
  width: 150px;
  font-size: 30px;
  background-color: yellow;
}


</style>
