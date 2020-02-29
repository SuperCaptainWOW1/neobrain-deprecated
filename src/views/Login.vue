<template>
  <div>
    <h2>Login</h2>
    <form @submit.prevent="login">
      <input v-model="email" type="text" name="email" />
      <br />
      <input v-model="password" type="password" name="password" />
      <br />
      <input type="submit" value="Login" />
    </form>
  </div>
</template>

<script>
import axios from 'axios';
// eslint-disable-next-line import/no-cycle
import router from '../router';

export default {
  name: 'Login',
  data: () => ({
    email: 'user@email.com',
    password: 'password',
  }),
  methods: {
    async login() {
      const loginData = {
        email: this.email,
        password: this.password,
      };

      try {
        // Make a variable for server path later
        await axios.post('http://localhost:3000/api/login', loginData, {
          withCredentials: true,
        });
        console.log('Logged in');
        router.push('/chat');
      } catch (err) {
        console.log(err);
        console.log('Cannot log in');
      }
    },
  },
};
</script>
