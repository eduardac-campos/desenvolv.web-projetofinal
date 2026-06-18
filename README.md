# Pizzaria do Bairro - Projeto Final de Desenvolvimento Web

Este projeto é uma evolução do sistema **T-Burguer**, reconstruído rigorosamente a partir da **base oficial (Professor/Projeto Final)**. Desenvolvido com **Vue 3**, o sistema foi adaptado para o segmento de **Pizzaria**.

## 🍕 Fidelidade Técnica e Metodologia
Conforme as regras da atividade, o projeto utiliza a estrutura de componentes e o ciclo de vida ensinados em sala:
- **Componentização:** Uso de `PedidoComponent.vue`, `ListaPedidoComponent.vue`, `BannerComponent.vue` e `NavBarComponent.vue` da base original.
- **Ciclo de Vida:** Utilização de `mounted` para chamadas de API e reatividade do Vue 3.
- **Estilização:** Manutenção do padrão visual da base, com adaptações de cores para o tema Pizzaria.

## 🛠️ Solução Técnica: Alertas Semânticos Reativos
Implementamos o `MessageComponent.vue` integrado aos componentes principais. A lógica de validação no `PedidoComponent.vue` garante que pedidos incompletos não sejam enviados:

```javascript
// Validação no PedidoComponent.vue
if(!this.nomeCliente || !this.pontoCarneSelecionado || !this.burguer) {
  this.msg = "Erro: Nome, Massa e Pizza são obrigatórios!";
  this.msgType = "error";
  setTimeout(() => this.msg = "", 3000);
  return;
}
```

## 🚀 UX e Fluxo de Navegação
- **Redirecionamento Inteligente:** Após a confirmação do pedido, o sistema exibe um alerta de sucesso e redireciona automaticamente para a tela de monitoramento após 2 segundos.
- **Atualização em Tempo Real:** A `ListaPedidoComponent.vue` foi aprimorada para re-renderizar a listagem imediatamente após a exclusão ou atualização de um pedido.

## 🔗 Links do Projeto
- **Repositório do Código:** [GitHub - desenvolv.web-projetofinal](https://github.com/eduardac-campos/desenvolv.web-projetofinal)
- **Repositório da API (JSON Server):** [GitHub - pizzaria-db](https://github.com/eduardac-campos/pizzaria-db)
- **API Mockada (Public):** [https://my-json-server.typicode.com/eduardac-campos/pizzaria-db](https://my-json-server.typicode.com/eduardac-campos/pizzaria-db)
- **Link de Produção:** [https://eduardac-campos.github.io/desenvolv.web-projetofinal/](https://eduardac-campos.github.io/desenvolv.web-projetofinal/)

---
*Projeto desenvolvido para a disciplina de Desenvolvimento Web, seguindo a base obrigatória do Professor.*
