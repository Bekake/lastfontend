<template>
    <div>
        <h1>{{ sending}} {{ pass }}</h1>
        <label >Username</label>
        <input type="text"  placeholder="Username"  v-model="sending"><br><br>
        <label for="password">Password</label>
        <input type="text" placeholder="Password" v-model="pass">
        <button @click="senddata">Send</button>
    </div>
    <hr>
    <div>
        <h1>{{myum[0]}} {{myum[1]}}</h1>
        <label >Username</label>
        <input type="text"  placeholder="Username"  v-model="myum[0]"><br><br>
        <label for="password">Password</label>
        <input type="text" placeholder="Password" v-model="myum[1]">
        <br><br>
        <button @click="umumiy">Send to umumiy</button>
        <p v-if="dont">Sent succesfully</p>
    </div>
</template>
  
<script>
import api from '@/services/api'
export default {
    data() {
        return {
        myum:[],
        message: '',
        sending: "",
        pass: "",
        dont: false
        };
    },
    mounted() {
        api.get('/')
        .then(response => {
            this.message = response.data;
        })
        .catch(error => {
            console.error(error);
        });
    },
    methods: {
        senddata() {
            api.post('/send', {
                user: [this.sending, this.pass],
            })
           .then(response => {
                if(response.status === 200){
                    this.$router.push('/data')
                }
            })
           .catch(error => {
                console.error(error);
            });
        },
        umumiy(){
            api.post('/umu', {
                tonext : this.myum,
            }).then( myres => {
                if(myres.status === 200){
                    this.dont = true
                }
            })
            .catch(error => {
                console.error(error)
            })
        }
    }
};
</script>
<style scoped>
label, input{
    padding: 0.4rem;
    border-radius: 5px;
    
}
input{
    border: 1px solid black;
}
    h1 {
        text-align: center;
    }
</style>
