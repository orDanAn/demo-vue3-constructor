<template>
  <div>
    <h2>
      {{value}}
    </h2>
  </div>
</template>

<script>
  export default {
    props: {
      value: {
      type:  String,
      required: true,
      }
    }
  }
</script>

<style lang="scss" scoped>

</style>