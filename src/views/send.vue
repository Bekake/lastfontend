<template>
<h1>Username: {{ message[0] }}</h1>
<h1>Password: {{ message[1] }}</h1>
</template>
<script>
import axios from 'axios';
export default {
    data(){
        return{
            message: ""
        }
        
    },
    mounted() {
        axios.get('http://localhost:5000/data')
        .then(response => {
            this.message = response.data;
        })
        .catch(error => {
            console.error(error);
        });
    },
}
</script>