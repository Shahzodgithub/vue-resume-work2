<template>
    <div class="card">
      <h2>Комментарии</h2>
      <ul class="list">
        <li class="list-item" v-for="(post,idx) in posts" :key="idx">
          <div>
            <p><strong> {{ post.email }} </strong></p>
            <small> {{ post.body }} </small>
          </div>
        </li>
      </ul>
    </div>
</template>

<script>
export default {
  props: ['posts']
};
</script>

<style scoped>
</style>