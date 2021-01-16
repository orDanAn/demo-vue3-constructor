<template>
  <h1>
    <slot>
      {{value}}
    </slot>
  </h1>
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

<style>

</style>