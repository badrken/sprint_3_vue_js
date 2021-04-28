<template>
  <base-card>
    <the-alert v-if="status == 'danger' || status=='success'" :status="status">
      {{ message }}
    </the-alert>
    <form @submit.prevent="signupSubmit">
      <h3 class="text-center mb-2">Sign Up</h3>

      <div class="form-group mb-2">
        <label class="mb-1">Full Name</label>
        <input v-model="fullName" type="text" class="form-control form-control-lg" />
      </div>

      <div class="form-group mb-2">
        <label class="mb-1">Email address</label>
        <input v-model="email" type="email" class="form-control form-control-lg" />
      </div>

      <div class="form-group mb-3">
        <label class="mb-1">Password</label>
        <input v-model="password" type="password" class="form-control form-control-lg" />
      </div>

      <input type="submit" class="btn btn-dark btn-lg mb-3 w-100" value="Sign Up" />

      <p class="text-end">
        Already registered
        <router-link to="/login">sign in?</router-link>
      </p>
    </form>
  </base-card>
</template>

<script>
import BaseCard from "@/components/BaseCard.vue";
import TheAlert from "@/components/TheAlert";
import axios from "axios";
import {v4 as uuid} from 'uuid';

export default {
 components: {
   BaseCard,
   TheAlert,
 },
 data() {
   return {
    fullName: '',
    email: '',
    password: '',
    status: '',
    message: '',
   }
 },
 methods: {
   async signupSubmit() {
     const {fullName, email, password} = this;
     try {
       if(!fullName || !email || !password) throw new Error('Please fill all fields');
       await axios.post('http://localhost:3000/users', {id: uuid(), name: this.fullName, email: this.email, password: this.password});
       setTimeout(() => {
          this.$router.push('/login');
        }, 1500);
        this.status = 'success';
        this.message = `Welcome ${this.fullName}`;
     } catch (err) {
       this.status = 'danger';
       this.message = err.message;
     }
   }
 }
}
</script>
