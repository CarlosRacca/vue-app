<template >
    <div id="temp">
        <div id="app">
            <div class="buttons">
                <button v-on:click="showContacts" class="buttonClicked" v-if="this.contactsClicked">Contacts</button>
                <button v-on:click="showContacts" class="buttonNotClicked" v-if="!this.contactsClicked">Contacts</button>
                <button v-on:click="showMessages" class="buttonClicked" v-if="this.messagesClicked">Messages</button>  
                <button v-on:click="showMessages" class="buttonNotClicked" v-if="!this.messagesClicked">Messages</button>  
            </div>
            <div v-if="this.viewContacts">
                <form action="" class="formContacts">
                    <input class="inputContacts" type="text" placeholder="Search...">
                </form>
                <div v-for="element in this.contacts" :key="element.id" class="contact" v-on:click="this.handleClickContact(element.id)">

                <h3 class="name" >
                    {{element.title}}
                </h3>
                </div>
            </div>
            <div v-if="this.viewMessages" >
                <div v-for="element in this.chats" :key="element.id" class="chats" v-on:click="this.handleClickChat(element.id)">
                    <h3>{{element.title}}</h3>
                    <h3>{{element.lastMessage}}</h3>
                </div>
            </div>
        </div> 
    </div>
</template>

<script>

export default {
    name: 'AllContacts',
    props: {
        contacts: Array,
        chats: Array
    },
    data() {
            return {
                api: [],
                allContacts: [],
                image: [],
                viewMessages: false,
                viewContacts: true,
                contactsClicked: true,
                messagesClicked: false,     
            }
        },
    mounted () {
        
    },
    watch: {
        
    },
    methods: {
        handleClickContact: function(id){
            this.$emit('contactClicked',id)
        },
        handleClickChat: function(id){
            this.$emit('chatClicked',id)
        },
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
    }
    
}
</script>

<style scoped>
    #app {
        background-color: rgb(119, 119, 154);
        display: flex;
        color: wheat;
        /* width: 300px; */
        /* height: 100%; */
        /* justify-content: right; */
        flex-direction: column;
        
    }

    #temp{
        display: flex;
        /* justify-content: flex-end; */
        background-color: violet;
        
    }

    .formContacts {
        padding: 5px;
        margin-left: 3px;
        margin-right: 10px;
    }

    .inputContacts {
        width: 100%;
        height: 50px;
        border-radius: 6px;
        font-size: 22px;
    }
    
    .inputContacts::placeholder{
        color: blueviolet;

    }



    .contact {
        background-color: red;
        margin: 8px;
        display: flex;
        
    }

    .chats {
        background-color: red;
        margin: 5px;
        display: flex;
        justify-content: space-around;
    }

    .name {
        margin-left: 10px;
    }
</style>