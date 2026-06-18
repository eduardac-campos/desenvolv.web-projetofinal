<template>
  <div class="message-container" :class="type" v-if="msg">
    <p>{{ msg }}</p>
  </div>
</template>

<script>
export default {
  name: "MessageComponent",
  props: {
    msg: String,
    type: {
      type: String,
      default: "success"
    }
  }
}
</script>

<style scoped>
  .message-container {
    border: 2px solid;
    border-radius: 5px;
    padding: 10px;
    max-width: 400px;
    margin: 30px auto;
    text-align: center;
    font-weight: bold;
  }

  .success {
    color: #155724;
    background-color: #d4edda;
    border-color: #c3e6cb;
  }

  .error {
    color: #721c24;
    background-color: #f8d7da;
    border-color: #f5c6cb;
  }

  .warning {
    color: #856404;
    background-color: #fff3cd;
    border-color: #ffeeba;
  }

  .info {
    color: #0c5460;
    background-color: #d1ecf1;
    border-color: #bee5eb;
  }
</style>
