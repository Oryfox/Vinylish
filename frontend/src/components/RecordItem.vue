<template>
  <div class="main" @click="navigateTo">
    <img :src="baseUrl + 'record/image?id=' + this.record.id" alt="Cover" />
    <div class="text-area">
      <span class="title">
        <b>{{ this.record.title }}</b>
      </span>
      <span class="artist">{{ this.record.artist }}</span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    record: { required: true },
  },
  data() {
    return {
      baseUrl: import.meta.env.VITE_HOST,
    };
  },
  methods: {
    navigateTo() {
      this.$router.push("/records/" + this.record.id);
    },
  },
};
</script>

<style scoped>
.main {
  height: 7rem;
  display: flex;
  align-items: center;
  border-radius: 1rem;
  transition-duration: 0.5s;
  cursor: pointer;
}
.main:hover {
  transition-duration: 0.5s;
  height: 15rem;
  font-size: x-large;
}
.text-area {
  display: flex;
  flex-direction: column;
  margin-left: 1rem;
}
img {
  width: auto;
  height: 90%;
  border-radius: 1rem;
  text-shadow: 2px 2px;
  filter: drop-shadow(2px 2px 3px rgba(0, 0, 0, 0.5));

  backface-visibility: hidden;
  transform: translate3d(0, 0, 0);
  -webkit-backface-visibility: hidden;
  -moz-backface-visibility: hidden;
  -webkit-transform: translate3d(0, 0, 0);
  -moz-transform: translate3d(0, 0, 0);
}
.title {
  font-size: inherit;
}
.artist {
  font-size: initial;
  color: var(--mild-color2);
}
.details {
  display: none;
}
.details-expand {
  display: inline-block;
}
</style>