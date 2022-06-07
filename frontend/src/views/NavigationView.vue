<template>
  <nav>
    <img src="/icon.png" alt="Logo" />
    <!--<RouterLink to="/" class="rl">Home</RouterLink>
    <RouterLink to="/about" class="rl">About</RouterLink>-->
    <div v-if="cookie" class="navb">
      <div
        @click="this.$router.go(-1)"
        class="back-button"
        v-if="
          this.$route.name !== 'records' &&
          this.$route.name !== 'artists' &&
          this.$route.name !== 'logout' &&
          this.$route.name !== 'login'
        "
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="16"
          height="16"
          fill="currentColor"
          class="bi bi-chevron-left"
          viewBox="0 0 16 16"
        >
          <path
            fill-rule="evenodd"
            d="M11.354 1.646a.5.5 0 0 1 0 .708L5.707 8l5.647 5.646a.5.5 0 0 1-.708.708l-6-6a.5.5 0 0 1 0-.708l6-6a.5.5 0 0 1 .708 0z"
          />
        </svg>
      </div>
      <RouterLink to="/records" class="rl"
        ><u v-if="this.$route.name === 'records'">Records</u
        ><span v-else>Records</span></RouterLink
      >
      <RouterLink to="/artists" class="rl"
        ><u v-if="this.$route.name === 'artists'">Artists</u
        ><span v-else>Artists</span></RouterLink
      >

      <div class="navbar-buttons">
        <div
          class="navbar-button"
          @click="createNew"
          v-if="this.$route.name === 'records'"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="22"
            height="22"
            fill="currentColor"
            class="bi bi-plus-circle"
            viewBox="0 0 16 16"
          >
            <path
              d="M8 15A7 7 0 1 1 8 1a7 7 0 0 1 0 14zm0 1A8 8 0 1 0 8 0a8 8 0 0 0 0 16z"
            />
            <path
              d="M8 4a.5.5 0 0 1 .5.5v3h3a.5.5 0 0 1 0 1h-3v3a.5.5 0 0 1-1 0v-3h-3a.5.5 0 0 1 0-1h3v-3A.5.5 0 0 1 8 4z"
            />
          </svg>
        </div>

        <div class="navbar-button" @click="this.$router.push('/logout')">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="22"
            height="22"
            fill="currentColor"
            class="bi bi-box-arrow-right"
            viewBox="0 0 16 16"
          >
            <path
              fill-rule="evenodd"
              d="M10 12.5a.5.5 0 0 1-.5.5h-8a.5.5 0 0 1-.5-.5v-9a.5.5 0 0 1 .5-.5h8a.5.5 0 0 1 .5.5v2a.5.5 0 0 0 1 0v-2A1.5 1.5 0 0 0 9.5 2h-8A1.5 1.5 0 0 0 0 3.5v9A1.5 1.5 0 0 0 1.5 14h8a1.5 1.5 0 0 0 1.5-1.5v-2a.5.5 0 0 0-1 0v2z"
            />
            <path
              fill-rule="evenodd"
              d="M15.854 8.354a.5.5 0 0 0 0-.708l-3-3a.5.5 0 0 0-.708.708L14.293 7.5H5.5a.5.5 0 0 0 0 1h8.793l-2.147 2.146a.5.5 0 0 0 .708.708l3-3z"
            />
          </svg>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
import emitter from "tiny-emitter/instance";
export default {
  props: {
    parent: null,
  },
  data() {
    return {
      cookie: null,
    };
  },
  created() {
    this.cookie = this.$cookies.get("token");
    emitter.on("tokenSet", (token) => (this.cookie = token));
    emitter.on("tokenRemove", () => (this.cookie = null));
  },
  methods: {
    createNew() {
      emitter.emit("createNew");
    },
  },
};
</script>

<style scoped>
nav {
  display: flex;
  background: #f0f0f0;
  height: 4rem;
  align-items: center;
}
.navb {
  display: flex;
  width: 100%;
}

.navbar-buttons {
  margin-left: auto;
  margin-right: 1rem;
  display: flex;
  gap: 0.5rem;
}

.navbar-button {
  border-radius: 1rem;
  width: 2rem;
  height: 2rem;
  display: flex;
  align-items: center;
  justify-content: center;
  transition-duration: 0.3s;
}
.navbar-button:hover {
  background: white;
  transition-duration: 0.3s;
}

.rl {
  text-decoration: none;
  border-radius: 1rem;
  color: #5f00a2;
  margin-right: 2rem;
  padding: 0.5rem 1rem;
  transition-duration: 0.3s;
}
.rl:hover {
  transition-duration: 0.3s;
  background: white;
}

.back-button {
  text-decoration: none;
  border-radius: 1rem;
  color: #5f00a2;
  margin-right: 2rem;
  display: flex;
  align-items: center;
  justify-content: center;
  transition-duration: 0.3s;
  width: 2.5rem;
  height: 2.5rem;
  cursor: pointer;
}
.back-button:hover {
  transition-duration: 0.3s;
  background: white;
}

img {
  width: auto;
  height: 80%;
  margin-right: 2rem;
  margin-left: 0.5rem;
}
</style>