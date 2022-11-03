<template>
  <div class="divGral">
    <SingleConversation 
      msg="Conversation" 
      :chat='this.chat'
      @chatModified='chatModified'
      @showContacts='showContacts'
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
      viewContacts: false,
      contactsClicked: true,
      messagesClicked: false,
      apiContacts: [],
      apiContactsCleaned: [],
      apiMessages: [],
      apiMessagesCleaned: [],
      contacts: [],
      chat: [],
      chatMod: [],
      varForChat: false
    }
  },
  async mounted () {    
    this.apiContacts = await axios.get("https://api.coloredstrategies.com/contacts")
    this.apiMessages = await axios.get('https://api.coloredstrategies.com/conversations')

  },
  methods: {
    chatModified: function () {
      this.chatMod = this.chat
      console.log('estoy en app, chatModified',this.chat)
      console.log('viendo los contacts',this.contacts)
    },

    showContacts: function(){

      this.viewContacts = true

      this.contactsClicked = true
      this.messagesClicked = false
    },

    chatSelected: function (id){
    
      this.chat = this.apiMessagesCleaned.filter(el => el.users[1] === id)[0]
      if(this.chat){
        
        this.chat.name = this.apiContactsCleaned.filter(el => el.id === id)[0].title
        this.chat.date = this.apiContactsCleaned.filter(el => el.id === id)[0].date
        this.chat.img = this.apiContactsCleaned.filter(el => el.id === id)[0].img
      }
    },

    contactSelected: function (id){
      
      this.chat = this.apiMessagesCleaned.filter(el => el.users[1] === id)[0]
      if(this.chat){
        
        this.chat.name = this.apiContactsCleaned.filter(el => el.id === id)[0].title
        this.chat.date = this.apiContactsCleaned.filter(el => el.id === id)[0].date
        this.chat.img = this.apiContactsCleaned.filter(el => el.id === id)[0].img

      }
      else{
        this.chat = {
          users: [1, id],
          date: this.apiContactsCleaned.filter(el => el.id === id)[0].date,
          name: this.apiContactsCleaned.filter(el => el.id === id)[0].title,
          img: this.apiContactsCleaned.filter(el => el.id === id)[0].img,
          id: this.apiMessagesCleaned.length + 1,
          messages: []
        }
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
    },

    chatMod: function(){
      console.log('watch chat, contacts',this.contacts)
      console.log('watch chat, chat',this.chat)
      let index = 0
      this.contacts.forEach(el => {
        if(this.chat.name === el.title){
          index = 1
          el.lastMessage = this.chat.lastMessageTime
        }
      })
      this.apiMessagesCleaned.forEach(element => {
        if(this.chat.users[1] === element.id){
          element = this.chat
        }
      })
      if(index === 0){
        this.contacts.push({
          date: this.chat.date,
          id: this.chat.users[1],
          lastMessage: this.chat.lastMessageTime,
          title: this.chat.name,
          img: this.chat.img
        })

        this.apiMessagesCleaned.push(this.chat)
      }

      this.varForChat = true

      console.log('api',this.apiMessagesCleaned)

      
    }
  }
}
</script>
    
<style>
#app {
  font-family:'Courier New', Courier, monospace;
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
  background-size: cover;
  min-height: 100%;
  text-align: center;
  color: #2c3e50;
  /* background-color: tomato; */
}

.buttons{
  
  display: flex;
  justify-content: flex-end;
  height: 100px;
  background-color: rgb(120, 150, 160);
  
  
}

.buttonClicked{
  font-family: 'Courier New', Courier, monospace;
  width: 150px;
  font-size: 25px;
  border: none;
  border-top: 10px solid rgb(30, 54, 73);
  color: rgb(30, 54, 73);
  background-color: rgb(120, 150, 160);
  padding-bottom: 12px;
}

.buttonNotClicked {
  font-family: 'Courier New', Courier, monospace;
  width: 150px;
  font-size: 25px;
  border: none;
  /* background-color: yellow; */
  background-color: rgb(120, 150, 160);
}

.divGral{
  display: flex;
  justify-content: space-between;
  
}


</style>
