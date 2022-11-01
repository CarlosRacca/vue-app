<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <!-- <HelloWorld msg="Welcome to Your Carlos.js App"/> -->
  <SingleConversation msg="Conversation"/>
  <AllContacts msg="Contacts"/>
  <AllChats msg="Chats"/>
  <TextBar msg="Text Bar"/>

</template>

<script>
import AllContacts from './components/AllContacts.vue'
import AllChats from './components/AllChats.vue'
import TextBar from './components/TextBar.vue'
import SingleConversation from './components/SingleConversation.vue'


export default {
  name: 'App',
  components: {
    SingleConversation,
    AllContacts,
    AllChats,
    TextBar
  }
}
</script>

    Contacts
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
