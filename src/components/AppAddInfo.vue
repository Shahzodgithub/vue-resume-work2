<template>
  <div class="container column">
    <form class="card card-w30" @submit.prevent="submitResume">
      <div class="form-control">
        <label for="type">Тип блока</label>
        <select id="type" v-model="resumeSelect">
          <option value="title">Заголовок</option>
          <option value="subtitle">Подзаголовок</option>
          <option value="avatar">Аватар</option>
          <option value="text">Текст</option>
        </select>
      </div>

      <div class="form-control">
        <label for="value">Значение</label>
        <textarea id="value" v-model.trim="textPlace" rows="3"></textarea>
      </div>

      <button :disabled="textLetter" class="btn primary">
        Добавить
      </button>
    </form>

    <div class="card card-w70">
      <div v-for="(obj, i) in formData" :key="i">
        <h1 v-if="obj.select === 'title'">{{ obj.data }}</h1>
        <div class="avatar" v-else-if="obj.select === 'avatar'">
          <img :src="obj.data" />
        </div>
        <h2 v-else-if="obj.select === 'subtitle'">{{ obj.data }}</h2>
        <p v-else>{{ obj.data }}</p>
      </div>
      <h3 v-if="defaultText">Добавьте первый блок, чтобы увидеть результат</h3>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      resumeSelect: "title",
      textPlace: "",
      src: '',
      defaultText: true,
      formData: [
        {
          data: "",
          select: "",
        },
      ],
    };
  },
  methods: {
    submitResume() {
      this.formData.push({
        data: this.textPlace,
        select: this.resumeSelect,
      });

      this.resumeSelect = "title";
      this.textPlace = "";
      this.defaultText = false
    }
  },
  computed: {
    textLetter() {
      return this.textPlace.length >= 3 ? false : true;
    },
  },
};
</script>

<style scoped>
</style>