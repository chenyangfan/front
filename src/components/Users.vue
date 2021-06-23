<template>
  <div class="container">
    <h3>Users:</h3>
    <table class="table">
      <thead>
      <tr>
        <th scope="col">First Name</th>
        <th scope="col">Last Name</th>
        <th scope="col">Email</th>
        <th scope="col">Phone Number</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="user in users" v-bind:key="user.id">
        <td>{{user.firstName}}</td>
        <td>{{user.lastName}}</td>
        <td>{{user.email}}</td>
        <td>{{user.phoneNumber}}</td>
      </tr>
      </tbody>
    </table>


    <div id="event">
      <button v-on:click="sort()">sort</button>
      <button v-on:click="search()">Search</button>
    </div>


    <form action="http://localhost:3000/contact" method="post">
      <div>
        <label for="say">first name</label>
        <input name="firstName" id="1" v-model="formData.firstName">
      </div>

      <div>
        <label for="say">last name</label>
        <input name="lastName" id="2" v-model="formData.lastName">
      </div>

      <div>
        <label for="say">Email</label>
        <input name="email" id="3" v-model="formData.email">
      </div>

      <div>
        <label for="say">phone</label>
        <input name="phoneNumber" id="4" v-model="formData.phoneNumber">
      </div>


      <div>
        <button>Submit</button>
      </div>
    </form>
  </div>
</template>
<script>
import axios from 'axios';
export default {
  name: 'Users',
  data() {
    return {
      users: null,
      formData: {
        firstName:'',
        lastName:'',
        email:'',
        phoneNumber:'',
      }
    };
  },
  created: function() {
    axios
        .get('http://localhost:3000/contacts')
        .then(res => {
          this.users = res.data;
        })
  },

  methods:{
    sort: function (){
      this.users.sort(function(a, b) {
        var nameA = a.lastName.toUpperCase(); // ignore upper and lowercase
        var nameB = b.lastName.toUpperCase(); // ignore upper and lowercase
        if (nameA < nameB) {
          return -1;
        }
        if (nameA > nameB) {
          return 1;
        }

        // names must be equal
        return 0;
      });
    },
  }
}
</script>
<style>
h3 {
  margin-bottom: 5%;
}
</style>