<template>
  <div id="app">
    {{ user.username }} - {{ fulName }} <strong>Followers: </strong>
    {{ followers }}
    <button @click="followUser">Follow</button>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      followers: 0,
      user: {
        id: 1,
        username: "@_GulRecep",
        firstName: "Recep",
        lastName: "Gül",
        email: "gulrecep29@icloud.com",
        isAdmin: true,
      },
    };
  },
  watch: {
    followers(newFollowerCount, oldFollowerCount) {
      if (oldFollowerCount < newFollowerCount) {
        console.log(`${this.fulName} takipçin arttı`);
      }
    },
  },
  computed: {
    fulName() {
      return `${this.user.firstName} ${this.user.lastName}`;
    },
  },

  methods: {
    followUser() {
      this.followers++;
    },
  },
  //bileşen ilk kez yüklendiğinde otomatik çalışır (onInit)
  mounted() {
    this.followUser();
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  display: flex;
  flex-direction: column;
  text-align: center;
}
</style>
