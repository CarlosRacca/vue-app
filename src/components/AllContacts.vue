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
                <form action="submit" class="formContacts" v-on:submit='handleSearch'>
                    <input name="search" class="inputContacts" type="text" placeholder="Search..." v-model="search">
                </form>

                <div v-if="this.contactsFiltered.length > 0">
                    <div v-for="element in this.contactsFiltered" :key="element.id" class="contact" v-on:click="this.handleClickContact(element.id)">

                    <h3 class="name" >
                        {{element.title}}
                    </h3>
                    </div>

                </div>
                <div v-else>
                    <div v-if="this.contactsFiltered.length === 0 && this.search.length > 0 ">
                        
                        <h3 class="noMatch" >
                            No contacts matching
                        </h3>

                    </div>
                    <div v-else>
                        <div v-for="element in this.contacts" :key="element.id" class="contact" v-on:click="this.handleClickContact(element.id)">

                        <h3 class="name" >
                            {{element.title}}
                        </h3>
                        </div>
                    </div>

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
                image: [],
                viewMessages: false,
                viewContacts: true,
                contactsClicked: true,
                messagesClicked: false,    
                search: '', 
                contactsFiltered: [],
                contactsRepeated: [],
                allChats: []
            }
        },
    mounted () {
        
    },
    watch: {
        search: function () {

            this.contactsFiltered = []

            this.contacts.forEach(el => {
                let mayus = el.title.toUpperCase()
                
                if(mayus.includes(this.search.toUpperCase())){
                    this.contactsFiltered.push(el)

                    this.contactsRepeated = this.contactsFiltered.filter(elem => el.title === elem.title)
                    if(this.contactsRepeated.length > 1){
                       this.contactsFiltered.pop()
                    }                    
                }
            })

        },

        
    },
    methods: {
        handleClickContact: function(id){
            this.$emit('contactClicked',id)
        },

        handleSearch: function (e) {
            e.preventDefault();

            console.log(this.search)
        },

        handleClickChat: function(id ){
            
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
        background-color: rgb(120, 150, 160);
        height: 100%;
        display: flex;
        color: rgb(30, 54, 73);
        /* width: 300px; */
        /* height: 100%; */
        /* justify-content: right; */
        flex-direction: column;
        height: 100vh;
        
    }

    #temp{
        display: flex;
        /* justify-content: flex-end; */
        /* background-color: rgb(120, 150, 160); */
        
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
        color: rgb(30, 54, 73);

    }



    .contact {
        border-radius: 5px;
        background-color: rgb(30, 54, 73);
        margin: 8px;
        display: flex;
        color:white;
        
    }

    .chats {
        border-radius: 5px;
        background-color: rgb(30, 54, 73);
        margin: 5px;
        display: flex;
        justify-content: space-around;
        color:white;
    }

    .name {
        margin-left: 10px;
    }

    .noMatch{
        padding-top: 300px;
        /* padding-bottom: 700px; */
    }
</style>