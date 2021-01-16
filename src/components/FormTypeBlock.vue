<template>
  <form class="card card-w30" @submit.prevent="submitForm">
      <div class="form-control">
        <label for="type">Тип блока</label>
        <select
          id="type"
          v-model="typeBlock"
        >
          <option value="TitleSummary">Заголовок</option>
          <option value="SubtitleSummary">Подзаголовок</option>
          <option value="Avatar">Аватар</option>
          <option value="Text">Текст</option>
        </select>
      </div>

      <div class="form-control">
        <label for="value">Значение</label>
        <textarea
          id="value"
          v-model="value"
          rows="3"
        ></textarea>
      </div>

      <button
        class="btn primary"
        :disabled="validationForm"
      >
        Добавить
      </button>
    </form>
</template>

<script>
export default {
  emits: {
    'submit-form'(obj) {
      if (Object.keys(obj).length) {
        return true
      }
      return false
    }
  },

  data() {
    return {
      typeBlock: 'TitleSummary',
      value: '',
    };
  },

  computed: {
    validationForm() {
      return !(this.value.length > 3)
    }
  },

  methods: {
    submitForm() {
      this.$emit('submit-form', { typeBlock: this.typeBlock, value: this.value});
      this.value = '';
      this.typeBlock = 'TitleSummary';
    }
  }
}
</script>

<style>

</style>