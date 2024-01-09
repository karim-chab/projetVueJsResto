<template>
  <img src="../assets/logo-resto.jpg" width="200" height="200" />
  <h1>Login</h1>
  <div class="login">
    <input type="text" v-model="email" placeholder="Enter Email" />
    <input type="password" v-model="password" placeholder="Enter Password" />
    <button @click="login">Login</button>
    <p>
      <router-link to="/sign-up">Sign up</router-link>
    </p>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: "Login", // eslint-disable-line vue/multi-word-component-names
  data()
  {
    return{
  email:'',
  password:''
    }
  },
  methods : {
    async login()
    {
        let result = await axios.get(
        `http://localhost:3000/users?email=${this.email}&password=${this.password}`
        )

        if(result.status==200 && result.data.length>0)
              {
                localStorage.setItem("user-info",JSON.stringify(result.data[0]))
                this.$router.push({name:'Home'})
              }
        console.warn(result)
    }
  },
   mounted()
  {
     let user= localStorage.getItem('user-info');
     if(user)
     {
       this.$router.push({name:'Home'})
     }
  }
};
</script>

<style>
.login input {
    width : 300px;
    height : 40px; 
    padding-left: 20px;
    display: block;
    margin-bottom: 30px;
    margin-right: auto;
    margin-left: auto;
    border: 1px solid skyblue; 

}
.login button {
    width: 320px;
    height: 40px;
    border: 1px solid skyblue;
    background: skyblue;
    color: #fff;
    cursor: pointer; 


}

</style>
