<template>
    <div class="container">
        <div class="row">
            <div class="col-5">
            <div class="card mt-4">
            <div class="card-body ">
                <form action="">
                    <label class="form-label" for="email">E-mail</label>
                    <input class="form-control" type="text" id="email" v-model="form.email">
                    <label class="form-label" for="pass">Contraseña</label>
                    <input class="form-control" type="password" id="pass" v-model="form.password">
                    <input class="btn btn-primary mt-2" type="button" @click="login" value="Ingresar"/>
                </form>
            </div>
            </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    data(){
        return {
            form:{
                email:'',
                password:''
            }
        }
    },
    methods: {
        login(){
            let formData = new URLSearchParams()
            formData.append('email',this.form.email)
            formData.append('password', this.form.password)
            axios.post('https://marco-mintic-58.herokuapp.com/login',formData,{
                headers:{
                    "Access-Control-Allow-Methods":"POST"
                }
            })
            .then((response)=>{
                // console.log(response)
                localStorage.setItem('token', response.data.token);
                this.$router.push('/home');
            })
        }
    }
}
</script>