<template>
<div class="loginwrapper">
  <form v-on:submit.prevent="errorMessage.length==0? validateForm():''" class="formwrapper">
    <h3 class="text-center titlesignup">Opret konto</h3>
    <div v-if="errorMessage" class="errormessage">
      <div v-for="error in errorMessage" v-bind:key="error.index">
        {{error}}
      </div>
    </div>
    <div class="userinputwrapper">
      <label for="firstname">
        <p>Fornavn</p>
        <input type="text" v-on:click="clearError" v-model="firstname" id="firstname" class="namesfield" value="" />
      </label>
    </div>
    <div class="userinputwrapper">
      <label for="lastname">
        <p>Efternavn</p>
        <input type="text" v-on:click="clearError" v-model="lastname" id="lastname" class="namesfield" value="" />
      </label>
    </div>
    <div class="userinputwrapper">
      <label for="email">
        <p>UCL Email</p>
        <input type="text" v-on:click="clearError" v-model="email" id="email" class="namesfield" value="" />
      </label>
    </div>
    <div>
      <label for="password">
        <p>Adgangskode</p>
        <input type="password" v-on:click="clearError" id="password" v-model="password" class="namesfield" value="" />
      </label>
    </div>
    <div><button type="submit" class="submitbtn">Submit</button></div>
    <!-- <span> Existing user?<router-link to='/signup'> Login</router-link></span> -->
  </form>
</div>
</template>
<script>
import Vue from 'vue';
export default Vue.extend({
    name:'SignUp',
    data(){
        return{
            firstname:'',
            lastname:'',
            email:"",
            password:'',
            errorMessage:[]
        }
    },
    methods:{
        validateForm(){
            console.log(history)
            if(this.firstname ==''){
                this.errorMessage.push('Udfyld fornavn')
            }
            if(this.password ==''){
                this.errorMessage.push(' Udfyld adgangskode')
            }
            if(this.lastname ==''){
                this.errorMessage.push(' Udfyld efternavn')
            }
            if(this.email==''){
                this.errorMessage.push(' Udfyld UCL Email')
                return
            }
            if(this.firstname !=='' && this.password !==''){
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
                firstname:this.firstname,
                lastname:this.lastname,
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
