<template>
  <div>
    <h1 id="menu-title">Monte a sua Pizza:</h1>
    <div id="scroll-horizontal">
      <div
        id="card-content"
        v-for="pizza in listaMenuPizzas"
        :key="pizza.id"
      >
        <div id="card-linha">
          <div class="foto-hamburguer">
            <img :src="pizza.foto" alt="nome da pizza" />
            <div class="card-coluna">
              <p id="nome-content">{{ pizza.nome }}</p>
              <p id="preco-content">R$ {{ pizza.valor }},00</p>
              <p id="descricao-content">{{ pizza.descricao }}</p>
              <button @click="selecionarPizza(pizza)">Escolher Sabor</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "MenuView",
  data() {
    return {
      listaMenuPizzas: [],
    };
  },
  methods: {
    async consultarMenu() {
      const response = await fetch(`${this.$apiUrl}/menu`);
      const dados = await response.json();
      this.listaMenuPizzas = dados.burgues;
    },
    selecionarPizza(pizzaSelecionada) {
      const param = JSON.stringify(pizzaSelecionada);
      const pizzaJson = encodeURIComponent(param);
      this.$router.push({ path: "/config", query: { burguer: pizzaJson } });
    },
  },
  mounted() {
    this.consultarMenu();
  },
};
</script>
<style scoped>
#menu-title {
  text-align: center;
  margin: 30px 0;
  font-size: 38px;
  color: #222;
}
#card-content {
  display: inline-block;
  width: 280px;
  min-height: 500px;
  margin: 20px;
  border: 1px solid #ddd;
  border-radius: 15px;
  box-shadow: 0 4px 8px #444;
  position: relative;
  overflow: hidden;
  vertical-align: top;
}
#scroll-horizontal {
  flex: 1;
  overflow-x: auto;
  white-space: nowrap;
  width: 90%;
  max-width: 1000px;
  margin: 0 auto;
  padding: 20px;
}
.foto-hamburguer img {
  width: 100%;
  object-fit: cover;
  height: 200px;
  border-radius: 10px 10px 0 0;
}
#nome-content {
  font-size: 25px;
  font-weight: bold;
  text-align: center;
  width: 100%;
  margin: 12px 0;
}
#preco-content {
  font-size: 35px;
  text-align: center;
  font-weight: bold;
  color: #2e7d32;
  margin: 16px 0;
}
#descricao-content {
  font-size: 14px;
  text-align: left;
  color: gray;
  margin: 16px;
  white-space: normal;
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 4;
  -webkit-box-orient: vertical;
  height: 80px;
}
.card-coluna button {
  padding: 12px;
  background-color: #222;
  color: #fcba03;
  font-weight: bold;
  border-radius: 8px;
  border: none;
  font-size: 16px;
  width: 80%;
  margin: 20px auto;
  display: block;
  cursor: pointer;
  transition: 0.5s;
}
.card-coluna button:hover {
  background-color: #fcba03;
  color: #222;
}
</style>
