<template>
  <div class="avatar">
    <img :src="value">
  </div>
</template>

<script>
export default {
  props: {
      value: {
      type:  String,
      required: true,
      validator: function (value) {
        const url = value;
        var valid = /^(ftp|http|https):\/\/[^ "]+$/.test(url);
        // Значение должно быть url
        return valid
      }
      }
    }

}
</script>

<style>

</style>