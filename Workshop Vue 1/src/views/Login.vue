<template>
  <base-card>
    <the-alert v-if="status == 'danger' || status=='success'" :status="status">
      {{ message }}
    </the-alert>
    <form @submit.prevent="loginSubmit">
      <h3 class="text-center">Sign In</h3>

      <div class="form-group mb-3">
        <label class="mb-1">Email address</label>
        <input
          v-model="email"
          type="email"
          class="form-control form-control-lg"
        />
      </div>

      <div class="form-group mb-3">
        <label class="mb-1">Password</label>
        <input
          v-model="password"
          type="password"
          class="form-control form-control-lg"
        />
      </div>

      <button type="submit" class="btn btn-dark btn-lg mb-4 w-100">
        Sign In
      </button>

      <p class="text-end mb-4">
        <router-link to="/forgot-password">Forgot password ?</router-link>
      </p>
    </form>
  </base-card>
</template>

<script>
import BaseCard from '@/components/BaseCard.vue';
import axios from 'axios';
import TheAlert from '@/components/TheAlert.vue';

export default {
  components: {
    BaseCard,
    TheAlert,
  },
  data() {
    return {
      email: '',
      password: '',
      status: '',
      message: '',
    };
  },
  methods: {
    async loginSubmit() {
      if (!this.email || !this.password) return;
      try {
        const user = await (
          await axios.get(
            `http://localhost:3000/users?email=${this.email}&password=${this.password}`
          )
        ).data;
        if (!user.length) throw new Error('Email or Password not correct, please try again!');
        setTimeout(() => {
          this.$router.push('/');
        }, 1500);
        this.status = 'success';
        this.message = 'login successfuly';
      } catch (err) {
        this.status = 'danger';
        this.message = err.message;
      }
    },
  },
};
</script>
