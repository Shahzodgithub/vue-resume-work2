<template>
  <div>
    <app-add-info></app-add-info>
    <div class="container">
      <p>
        <button class="btn primary" @click="getPosts" v-if="got">
          Загрузить комментарии
        </button>
      </p>
      <div class="loader" v-if="loading"></div>
      <app-comments :posts="posts" v-else></app-comments>
    </div>
  </div>
</template>

<script>
import AppAddInfo from "./components/AppAddInfo.vue";
import AppComments from "./components/AppComments.vue";
export default {
  data() {
    return {
      loading: false,
      posts: null,
      got: true,
    };
  },
  components: {
    AppAddInfo,
    AppComments,
  },
  methods: {
    async getPosts() {
      this.loading = true;
      const res = await fetch(
        "https://jsonplaceholder.typicode.com/comments?_limit=42"
      );
      this.posts = await res.json();

      this.got = false;
      this.loading = false;
    },
  },
};
</script>

<style>
.avatar {
  display: flex;
  justify-content: center;
}

.avatar img {
  width: 150px;
  height: auto;
  border-radius: 50%;
}
</style>
