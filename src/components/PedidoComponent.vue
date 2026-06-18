<template>
  <div>
    <MessageComponent :msg="msg" :type="msgType" v-show="msg" />
    <form id="form-pedido" @submit="criarPedido">
      <div>
        <p id="nome-hamburguer-content">{{ burguer && burguer.nome ? burguer.nome : 'Selecione uma Pizza' }}</p>
        <img
          id="foto-content"
          :src="burguer && burguer.foto ? burguer.foto : ''"
        />
      </div>
      <div class="inputs">
        <label for="nome-cliente">Nome do Cliente</label>
        <input
          type="text"
          v-model="nomeCliente"
          id="nome-cliente"
          name="nome-cliente"
          placeholder="Digite seu Nome"
        />
      </div>
      <div class="inputs">
        <label>Tipo de Massa</label>
        <select
          name="ponto-carne"
          id="ponto-carne"
          v-model="pontoCarneSelecionado"
        >
          <option value="" selected>Selecione a massa</option>
          <option
            v-for="pontoCarne in listaPontoCarne"
            :key="pontoCarne.id"
            :value="pontoCarne"
          >
            {{ pontoCarne.descricao }}
          </option>
        </select>
      </div>
      <div class="inputs">
        <label id="opcionais-titulo"> Selecione os opcionais</label>
        <label id="opcionais-subtitulo"> Adicionais e Bordas</label>
        <div
          class="checkbox-container"
          v-for="complemento in listaComplementos"
          :key="complemento.id"
        >
          <input
            type="checkbox"
            :name="complemento.nome"
            :value="complemento"
            v-model="listaComplementosSelecionados"
          />
          <span>{{ complemento.nome }}</span>
        </div>
        <label> Adicione uma bebida</label>
        <div
          class="checkbox-container"
          id="checkbox-container"
          v-for="bebida in listaBebidas"
          :key="bebida.id"
        >
          <input
            type="checkbox"
            :name="bebida.nome"
            :value="bebida"
            v-model="listaBebidasSelecionadas"
          />
          <span>{{ bebida.nome }}</span>
        </div>
        <div class="inputs">
          <input type="submit" class="submit-btn" value="Confirmar Pedido de Pizza" />
        </div>
      </div>
    </form>
  </div>
</template>
<script>
import MessageComponent from './MessageComponent.vue';

export default {
  name: "PedidoComponent",
  props: {
    burguer: null,
  },
  components: {
    MessageComponent
  },
  data() {
    return {
      listaPontoCarne: [],
      listaBebidas: [],
      listaComplementos: [],
      nomeCliente: "",
      pontoCarneSelecionado: "",
      listaComplementosSelecionados: [],
      listaBebidasSelecionadas: [],
      msg: null,
      msgType: null
    };
  },
  methods: {
    async getTipoPontos() {
      const response = await fetch(`${this.$apiUrl}/tipos_pontos`);
      const dados = await response.json();
      this.listaPontoCarne = dados;
    },
    async getOpcionais() {
      const response = await fetch(`${this.$apiUrl}/opcionais`);
      const dados = await response.json();
      this.listaComplementos = dados.complemento;
      this.listaBebidas = dados.bebidas;
    },
    async criarPedido(e) {
      e.preventDefault();

      // Validação
      if(!this.nomeCliente || !this.pontoCarneSelecionado || !this.burguer) {
        this.msg = "Erro: Nome, Massa e Pizza são obrigatórios!";
        this.msgType = "error";
        setTimeout(() => this.msg = "", 3000);
        return;
      }

      const dadosPedido = {
        nome: this.nomeCliente,
        ponto: this.pontoCarneSelecionado,
        bebidas: Array.from(this.listaBebidasSelecionadas),
        complemento: Array.from(this.listaComplementosSelecionados),
        burguer: this.burguer,
        statusId: 1,
      };

      const dadosJson = JSON.stringify(dadosPedido);
      const req = await fetch(`${this.$apiUrl}/pedidos`, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: dadosJson,
      });

      const res = await req.json();

      // Feedback de Sucesso
      this.msg = `Sucesso: Pedido Nº ${res.id} realizado!`;
      this.msgType = "success";

      // Redirecionamento Inteligente
      setTimeout(() => {
        this.msg = "";
        this.$router.push("/pedidos");
      }, 2000);
    },
  },
  mounted() {
    this.getTipoPontos();
    this.getOpcionais();
  },
};
</script>
<style scoped>
#foto-content {
  margin-bottom: 16px;
  border-radius: 16px;
  position: relative;
  z-index: -1;
  justify-content: center;
  width: 100%;
  height: 180px;
  object-fit: cover;
}
#nome-hamburguer-content {
  font-size: 43px;
  font-weight: bold;
  text-align: start;
  margin-bottom: -90px;
  margin-left: 40px;
  color: antiquewhite;
  padding: 16px;
  text-shadow: 2px 2px 4px #000;
}
#form-pedido {
  max-width: 750px;
  margin: 0 auto;
}
.inputs {
  display: flex;
  flex-direction: column;
  margin-bottom: 16px;
}
label {
  font-weight: bold;
  margin-bottom: 16px;
  color: #222;
  padding: 5px 12px;
  flex-direction: start;
  display: flex;
  border-left: 4px solid #fcba03;
}
input,
select {
  padding: 12px;
  width: 300px;
  border: solid #222 1px;
  border-radius: 8px;
  height: 20px;
  font-size: 12px;
}
select {
  height: 45px;
}
#opcionais-titulo {
  width: 100%;
}
#opcionais-subtitulo {
  display: flex;
  align-items: flex-start;
  align-content: center;
  width: 100%;
  margin-bottom: 12px;
}
.checkbox-container span {
  margin-left: 6px;
  font-weight: bold;
}
.checkbox-container span,
.checkbox-container input {
  width: auto;
  height: 20px;
}
.submit-btn {
  background-color: #222;
  color: #fcba03;
  font-weight: bold;
  border: none;
  font-size: 18px;
  border-radius: 12px;
  padding: 16px;
  margin: 0 auto;
  cursor: pointer;
  width: 100%;
  height: auto;
  transition: 0.5s;
}
.submit-btn:hover {
  background-color: #fcba03;
  color: #222;
}
</style>
