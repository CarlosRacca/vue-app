<template>
  <button v-on:click="showContacts">Contacts</button>
  <button v-on:click="showMessages">Messages</button>
  
  <!-- <HelloWorld msg="Welcome to Your Carlos.js App"/> -->
  
  <AllContacts classname='Contacts' v-if="viewContacts" msg="Contacts" :contacts="this.apiContactsCleaned"/>
  <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
  <AllChats v-if="viewMessages" msg="Chats" :chats='this.contacts'/>
  <SingleConversation msg="Conversation"/>
  <TextBar msg="Text Bar"/>

</template>

<script>
import AllContacts from './components/AllContacts.vue'
import AllChats from './components/AllChats.vue'
import TextBar from './components/TextBar.vue'
import SingleConversation from './components/SingleConversation.vue'
import axios from 'axios'


export default {
  name: 'App',
  components: {
    SingleConversation,
    AllContacts,
    AllChats,
    TextBar
  },
  data () {
    return {
      viewMessages: false,
      viewContacts: true,
      apiContacts: [],
      apiContactsCleaned: [],
      apiMessages: [],
      apiMessagesCleaned: [],
      contacts: []
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
    },
    showMessages: function(){
      if(this.viewContacts){
        this.viewContacts = false
      }
      this.viewMessages = true
    },
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
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}


</style>
