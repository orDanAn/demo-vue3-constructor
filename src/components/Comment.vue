<template>
  <h2>Комментарии</h2>
      <ul class="list">
        <li
          class="list-item"
          v-for="comment in comments"
          :key="comment.id"
        >
          <div>
            <p><strong>{{comment.email}}</strong></p>
            <small>{{comment.body}}</small>
          </div>
        </li>
      </ul>
</template>

<script>
export default {
  // body email id: 1 name: "id l
  props: {
    comments: Array,
  }
}
</script>

<style>

</style>