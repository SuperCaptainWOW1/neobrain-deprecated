<template>
  <div>
    <h2>Chat. User: {{ user.name }}</h2>
    <div class="friends">
      <div v-for="friend in user.friends" :key="friend.name">
        <p>{{ friend.name }}</p>
        <span>{{ friend.online ? 'в сети' : 'не в сети' }}</span>
      </div>
    </div>
    <div class="chat"></div>
  </div>
</template>

<script>
import router from 'vue-router';

export default {
  name: 'Chat',
  data: () => ({
    user: {
      name: 'Oleg',
      friends: [
        {
          name: 'Vosyan',
          online: true,
        },
      ],
    },
  }),
  methods: {
    async getUserData() {
      try {
        const user = await fetch('api/user');
        this.user = await user;
      } catch (err) {
        console.log(err);
        router.push('/');
      }
    },
  },
  mounted() {
    this.getUserData();
  },
};
</script>
