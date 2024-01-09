<template>
<Header />
    <h1>Hello user, Welcome on Add restaurant Page</h1>
    <form class="add">
      <input type="text" name ="name" placeholder="Enter Name" v-model="restaurant.name"/>
      <input type="text" name="address" placeholder="Enter address" v-model="restaurant.address"/>
      <input type="text" name="contact" placeholder="Enter contact" v-model="restaurant.contact"/>
      <button type="button" v-on:click="addRestaurant">Add new Restaurant </button>

     </form>
</template>
<script>
import Header from './Header.vue';
import axios from 'axios';
export default {
 name:'Add' , // eslint-disable-line vue/multi-word-component-names
 components:{
  Header  // eslint-disable-line vue/multi-word-component-names
 },
 data()
 {
    return {
      restaurant :{
        name:'',
        address:'',
        contact:''


      }
    }
 },
 methods:{
  async addRestaurant()
  {
    console.warn(this.restaurant)
    const result = axios.post("http://localhost:3000/restaurant",{
       name:this.restaurant.name,
       address:this.restaurant.address,
       contact:this.restaurant.contact,


    });
    if(result.status==201)
    {
      this.$router.push({name:'Home'})
    }
    console.warn("result",result)
  }

 },
 mounted()
  {
     let user= localStorage.getItem('user-info');
     
     if(!user)
     {
       this.$router.push({name:'SignUp'})
     }
  }      
}
</script>
<style>
.add input {
    width : 300px;
    height : 40px; 
    padding-left: 20px;
    display: block;
    margin-bottom: 30px;
    margin-right: auto;
    margin-left: auto;
    border: 1px solid skyblue; 

}
.add button {
    width: 320px;
    height: 40px;
    border: 1px solid skyblue;
    background: skyblue;
    color: #fff;
    cursor: pointer; 


}

</style>
