<template >
    <div id="temp">
        <div id="app">
            <h1>{{ msg }}</h1>
                <form action="">
                    <input type="text" placeholder="Search...">
                </form>
            <div v-for="element in this.contacts" :key="element.id" class="contact" v-on:click="this.handleClick(element.id)">

            <h3 class="name" >
                {{element.title}}
            </h3>
            </div>
        </div> 
    </div>
</template>

<script>

export default {
    name: 'AllContacts',
    props: {
        msg: String,
        contacts: Array,
    },
    data() {
            return {
                api: [],
                allContacts: [],
                image: [],
                
            }
        },
    mounted () {
        
    },
    watch: {
        
    },
    methods: {
        handleClick: function(id){
            this.$emit('contactClicked',id)
        }
    }
    
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
        flex-direction: column;
        
    }

    #temp{
        display: flex;
        justify-content: end;
        background-color: violet;
        
    }

    .contact {
        background-color: red;
        margin: 8px;
        display: flex;
        
    }

    .name {
        margin-left: 10px;
    }
</style>