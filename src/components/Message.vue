<template>
  <div class="message">
    <p>{{ message }}</p>
  </div>
</template>

<script>
export default {
  name:"Message",
  props: {
    message: {
      type: String,
      require: true
    }
  }
}
</script>

<style lang="scss" scoped>
  .message {
    text-align: center;
    padding: 20px;
    color: red;
  }
</style>