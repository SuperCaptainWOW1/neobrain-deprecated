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
import router from 'vue-router';

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
        await fetch('/api/login', {
          method: 'POST',
          body: loginData,
        });
        console.log('Logged in');
        router.push('/chat');
      } catch (err) {
        console.log('Cannot log in');
      }
    },
  },
};
</script>
