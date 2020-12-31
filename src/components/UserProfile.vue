<template>
  <div class="user-profile">
    <div class="user-profile__user-panel">
      <h1 class="user-profile__username">@{{ user.username }}</h1>
      <div class="user-profile__admin-badge">Admin</div>
      <div class="user-profile__follower-count">
        <strong>Followers: </strong> {{ followers }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "UserProfile",

  data() {
    return {
      followers: 0,
      user: {
        id: 1,
        username: "_GulRecep",
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
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  width: 100%;
  padding: 50px 5%;
}

.user-profile__user-panel {
  display: flex;
  flex-direction: column;
  margin-right: auto;
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #dfe3e8;
}
h1 {
  margin: 0;
}
.user-profile__admin-badge {
  background: rgb(135, 19, 180);
  color: white;
  border-radius: 5px;
  margin-right: auto;
  padding: 0 10px;
  font-weight: bold;
}
</style>