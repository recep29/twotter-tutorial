<template>
  <div class="user-profile">
    <div class="user-profile__user-panel">
      <h1 class="user-profile__username">@{{ user.username }}</h1>
      <div class="user-profile__admin-badge" v-if="user.isAdmin">Admin</div>

      <div class="user-profile__follower-count">
        <strong>Followers: </strong> {{ followers }}
      </div>
    </div>
    <div class="user-profile__twoots-wrapper">
      <twoot-item
        v-for="twoot in user.twoots"
        :key="twoot.id"
        :username="user.username"
        :twoot="twoot"
        @favourite="toggleFavourite"
      />
    </div>
  </div>
</template>

<script>
import TwootItem from "./TwootItem.vue";

export default {
  components: { TwootItem },
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
        twoots: [
          {
            id: 1,
            content: "Twotter is Amazing!",
          },
          {
            id: 2,
            content: "Kullanışlı bir programdir.",
          },
        ],
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
    toggleFavourite(id) {
      console.log(`favorite tweet #${id}`);
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
  grid-gap: 50px;
  padding: 50px 5%;
}

.user-profile__user-panel {
  display: flex;
  flex-direction: column;
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #dfe3e8;
  margin-bottom: auto;
}
h1 {
  margin: 0;
}

.user-profile__admin-badge {
  background: rebeccapurple;
  color: white;
  border-radius: 5px;
  margin-right: auto;
  padding: 0 10px;
  font-weight: bold;
}
.user-profile__twoots-wrapper {
  display: grid;
  grid-gap: 10px;
  margin-bottom: auto;
}
</style>