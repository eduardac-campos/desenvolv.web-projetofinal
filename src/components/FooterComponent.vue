<template>
  <footer id="footer">
    <p>Pizzaria do Bairro &copy; 2026</p>
  </footer>
</template>

<script>
export default {
  name: "FooterComponent"
}
</script>

<style scoped>
  #footer {
    height: 150px;
    background-color: #222;
    border-top: 4px solid #111;
    color: #fcba03;
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100%;
    margin-top: 50px;
  }
</style>
