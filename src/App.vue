<template>
  <div class="container column">
    <FormTypeBlock
      @submit-form="submitForm"
    />

    <div class="card card-w70">
      <div v-if="blocks.length">
        <component v-for="item in blocks" :key="item.id" :is="item.typeBlock" :value="item.value"> 
        </component>
      </div>
      
      <h3
        v-else
      >
        Добавьте первый блок, чтобы увидеть результат
      </h3>
    </div>
  </div>
  <div class="container">
    <p>
      <button
        v-if="showButton"
        class="btn primary"
        @click="readComent"
      >
        Загрузить комментарии
      </button>
    </p>
    <div class="card" v-if="hasError">
      <h3 style="color: red"   >
      Произошла ошибка при запросе. Попробуйте ещё раз
    </h3>
    </div>
    <Loader
      v-if="loading"
    />
    <div class="card" v-if="comments.length">
      <Comment
        :comments="comments"
      />
    </div>
    
  </div>
</template>

<script>
import FormTypeBlock from '@/components/FormTypeBlock.vue';
import TitleSummary from '@/components/TitleSummary.vue';
import SubtitleSummary from './components/SubtitleSummary.vue';
import Avatar from './components/Avatar.vue';
import Text from './components/Text.vue';
import Comment from './components/Comment.vue';
import Loader from './components/Loader.vue';


export default {
  data() {
    return {
      blocks: [],
      comments: [],
      loading: false,
      hasError: false,
    };
  },

  computed: {
    showButton() {
      if (this.comments.length) {
        return false;
      }
      if (this.loading) {
        return false;
      }
      return true;
    }
  },

  methods: {
    submitForm(obj) {
      const {typeBlock, value} = obj;
      const itemComponents = {
        typeBlock,
        value,
        id: new Date().getMilliseconds(),
      }
      this.blocks.push(itemComponents);
    },

    async readComent() {
      try {
        this.loading = true;
        const response = await fetch('https://jsonplaceholder.typicode.com/comments?_limit=42');
        const result = await response.json();
        this.comments = [...result];
        this.loading = false;
      } catch (e) {
        console.error(e);
        this.hasError = true;
        this.loading = false;
      }
    }
  },

  components: {
    FormTypeBlock,
    TitleSummary,
    SubtitleSummary,
    Avatar,
    Text,
    Comment,
    Loader,
  }


}
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
