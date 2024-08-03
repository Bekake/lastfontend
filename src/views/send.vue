<template>
<h1>Username: {{ message[0] }}</h1>
<h1>Password: {{ message[1] }}</h1>
</template>
<script>
import api from '@/services/api'
export default {
    data(){
        return{
            message: ""
        }
        
    },
    mounted() {
        api.get('/data')
        .then(response => {
            this.message = response.data;
        })
        .catch(error => {
            console.error(error);
        });
    },
}
</script>