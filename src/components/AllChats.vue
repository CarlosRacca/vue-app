<template>
    <div id='temp'>
        <div id="app">
            <h1>{{ msg }}</h1>
            <div v-for="element in this.chats" :key="element.id" class="chats">
                <h3>{{element.title}}</h3>
                <h3>{{element.lastMessage}}</h3>
            </div>
        </div>
    </div>
</template>

<script>

export default {
    name: 'AllChats',
    props: {
        msg: String,
        chats: Array
    },
    data() {
            return {
                api: [],
                conversations: [],
                contacts: [],
                users: []
                
            }
        },
    mounted () {
        
    },
}
</script>

<style scoped>
    #app {
        background-color: rgb(119, 119, 154);
        display: flex;
        color: wheat;
        width: 300px;
        height: 100%;
        justify-content: right;
        /* align-content: center; */
        flex-direction: column;
        
    }

    #temp{
        display: flex;
        justify-content: end;
        background-color: violet;
        
    }

    .chats {
        background-color: red;
        margin-bottom: 5px;
        margin-top: 5px;
        display: flex;
        justify-content: space-around;
    }
</style>