<template>
<div>
  <h3 class="text-center">Schedule</h3>
  <hr>  
  <div class="container">
    <form v-on:submit.prevent="createContact">   
    <div class="row"> 
    <div class="col-md-4">
      <input v-mask="['(##) #####-####', '(##) ####-####']" class="form-control" name="phone" type="text" v-model="contact.phone" placeholder="Type phone here" />
      <p v-show="errors.phone.visible" class="text-danger">{{errors.phone.message}}</p>
    </div>
    <div class="col-md-4">
      <input class="form-control" name="name" type="text" v-model="contact.name" placeholder="Type name here" />
      <p v-show="errors.name.visible" class="text-danger">{{errors.name.message}}</p>
    </div>
    <div class="col-md-4"> 
      <button type="submit" class="btn btn-success">Create</button>
    </div>
    </div>
    </form>
    <div class="row">
    <div class="col-md-4" v-for="(item, index) in contacts" v-bind:key="item">
      <div class="card card-contact">
        <h6><i class="fa fa-phone" /> {{item.phone}}</h6>
        <h6><i class="fa fa-user" /> {{item.name}}</h6>
        <button class="btn btn-danger" v-on:click="deleteContact(index)">Delete</button>
      </div>
    </div>
    </div>
  </div>
</div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.css"
import "font-awesome/css/font-awesome.css"
import {mask} from 'vue-the-mask'


export default {
  name: 'app',
  data(){
    return{ 
      contacts: [],
      contact: {
        "name": '',
        "phone": ''                
      },
      errors:{
        name:{
          'visible': false,
          'message': 'Please type a name'
        },
        phone:{
          'visible': false,
          'message': 'Please type a phone'
        }
      }
    }
  },
  methods: {
    createContact(){  

      if(this.contact.phone === '')
      {
        this.errors.phone.visible = true;
        return;
      }

      if(!this.contact.name === '')
      {
        this.errors.name.visible = true;
        return;
      }

      this.contacts.push({...this.contact});
      this.contact.name = '';
      this.contact.phone = '';
      this.errors.name.visible = false;
      this.errors.phone.visible = false;
    },
    deleteContact(index){
      this.contacts.splice(index, 1);
    },
  },
  directives: {mask}
}
</script>

<style>
#slogan{
  text-align: center;
}
form{
  width: 100%;
  margin-bottom: 2%;
}
.card-contact{
  padding: 5%;
}
</style>
