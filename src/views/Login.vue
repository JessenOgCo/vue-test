<template>
    <div class="loginwrapper">
          <form v-on:submit.prevent ="errorMessage.length==0? validateForm():''" class="formwrapper">
                <h3 class="text-center titlesignup">Log ind</h3>
                <div v-if="errorMessage" class="errormessage">
                   <div v-for="error in errorMessage" v-bind:key="error.index">
                    {{error}}
                   </div>
                </div>
                <div class="userinputwrapper">
                  <label for="username">
                    <p>UCL email</p>
                    <input type="text" v-on:click="clearError" v-model="username" id="username" class="namesfield" value="" />
                  </label>
                </div>
                <div>
                  <label for="password">
                    <p>Adgangskode</p>
                    <input type="password" v-on:click="clearError" id="password" v-model="password" class="namesfield" value="" />
                  </label>
                </div>
                <div>
                  <button type="submit" class="submitbtn">Log ind</button>
                </div>
                <div class="signup">
                  <span> Ny bruger?<router-link to='/signup'> Opret konto</router-link></span>
                </div>
          </form>
    </div>
</template>
<script>
import Vue from 'vue';
export default Vue.extend({
    name:'Login',
    data(){
        return{
            username:'',
            password:'',
            errorMessage:[]
        }
    },
    methods:{
        validateForm(){
            console.log(history)
            if(this.username ==''){
                this.errorMessage.push(' Udfyld UCL mail')
            }
            if(this.password ==''){
                this.errorMessage.push(' Udfyld Password')
                return
            }
            if(this.username !=='' && this.password !==''){
                this.submitForm()
            }
            console.log(this.errorMessage)
        },
        clearError(){
            console.log('form fields cleared')
            this.errorMessage=[]
        },
        submitForm(){
            const data = {
                email:this.username,
                password:this.password
            }
            console.log(data)
            localStorage.setItem('userinfo', JSON.stringify(data)) //in the absence of a real api for user auth this would handle auth
            alert('Form Submitted')
            //make network request
            //axios post
            this.$router.push('/dashboard')
        }
    }
})
</script>

<style>

</style>
