<template>
  <div class="divGral">
    <SingleConversation 
      msg="Conversation" 
      :chat='this.chat'
    />  
    <AllContacts 
      classname='Contacts' 
      v-if="viewContacts"
      :contacts="this.apiContactsCleaned" 
      :chats='this.contacts' 
      @contactClicked='contactSelected' 
      @chatClicked='chatSelected'
    />
  </div>
</template>

<script>
import axios from 'axios'

import AllContacts from './components/AllContacts.vue'
import SingleConversation from './components/SingleConversation.vue'


export default {
  name: 'App',
  components: {
    SingleConversation,
    AllContacts,

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

    chatSelected: function (id){
      
      this.chat = this.apiMessagesCleaned.filter(el => el.users[1] === id)[0]
      if(this.chat){
        
        this.chat.name = this.apiContactsCleaned.filter(el => el.id === id)[0].title
      }
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
  background-color: tomato;
}

.buttons{
  display: flex;
  justify-content: flex-end;
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

.divGral{
  display: flex;
  justify-content: space-between;
  
}


</style>
