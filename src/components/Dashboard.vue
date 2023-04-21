<template>
  <div id="churro-table">
    <Message :msg="msg" v-show="msg" />
    <div>
      <div id="churro-table-heading">
        <div class="order-id">N°</div>
        <div class="colunas">Cliente:</div>
        <div class="colunas">Recheio</div>
        <div class="colunas">Cobertura</div>
        <div class="colunas">Acompanhamento</div>
        <div class="colunas">Adicionais</div>
        <div class="colunas">Ações</div>
      </div>
    </div>
    <div id="churro-table-rows">
      <div id="churro-table-row" v-for="churro in churros" :key="churro.id">
        <div class="order-number">{{ churro.id }}</div>
        <div>{{ churro.nome }}</div>
        <div>{{ churro.recheio }}</div>
        <div>{{ churro.cobertura }}</div>
        <div>{{ churro.acompanhamento }}</div>
        <div>
          <ul class="lista-adicionais">
            <li v-for="(adicional, index) in churro.adicionais" :key="index">
              {{ adicional }}
            </li>
          </ul>
        </div>
        <div id="acoes">
          <select  name="status"  class="status"  @change="updateChurro($event, churro.id)">
            <option :value="s.tipo"  v-for="s in status"  :key="s.id"  :selected="churro.status == s.tipo">
              {{ s.tipo }}
            </option>
          </select>
          <button class="delete-btn" @click="deleteChurro(churro.id)">
            Cancelar
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Message from './Message.vue';
export default {
  name: "Dashboard",
  data() {
    return {
      churros: null,
      churros_id: null,
      status: [],
      msg: null,
    };
  },
  methods: {
    async getPedidos() {
      const req = await fetch("http://localhost:3000/churros");
      const data = await req.json();

      this.churros = data;
      //resgatar os status
      this.getStatus();
    },
    async getStatus() {
      const req = await fetch("http://localhost:3000/status");
      const data = await req.json();
      this.status = data;
    },
    async deleteChurro(id) {
      const req = await fetch(`http://localhost:3000/churros/${id}`, {
        method: "DELETE",
      });

      const res = await req.json();
      this.msg = `Pedido N°${id} foi removido!`;
      //limpar mesagem
      setTimeout(() => (this.msg = ""), 3000);
      //msg "pedido deletado"

      this.getPedidos();
    },
    async updateChurro(event, id) {
      const option = event.target.value;
      const dataJson = JSON.stringify({ status: option });
      const req = await fetch(`http://localhost:3000/churros/${id}`, {
        method: "PATCH",
        headers: { "Content-Type": "application/json" },
        body: dataJson,
      });
      const res = await req.json();
      this.msg = `Pedido N°${res.id} foi atualizado para ${res.status}`;
      //limpar mesagem
      setTimeout(() => (this.msg = ""), 3000);
    },
  },
  mounted() {
    this.getPedidos();
  },
  components:{
    Message,
  }
};
</script>

<style scoped>
#churro-table {
  max-width: 1250px;
  margin: 0 auto;
}

#churro-table-heading,
#churro-table-rows,
#churro-table-row {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}

#churro-table-heading {
  font-weight: bold;
  padding: 12px;
  border-bottom: 3px solid var(--preto);
}
#churro-table-heading div,
#churro-table-row div {
  width: 15%;
}

#churro-table-row {
  width: 100%;
  padding: 12px;
  border-bottom: 1px solid var(--branco);
}
#churro-table-heading .order-id,
#churro-table-row .order-number {
  width: 5%;
}

select {
  padding: 12px 6px;
  margin-right: 12px;
}
#acoes {
  display: flex;
}

.delete-btn {
  background-color: var(--preto);
  color: var(--amarelo);
  font-weight: bold;
  border: 2px solid var(--preto);
  padding: 10px;
  font-size: 16px;
  margin: 0 auto;
  cursor: pointer;
  transition: 0.5s;
}
.lista-adicionais li {
  text-decoration: dotted;
}

.delete-btn:hover {
  background-color: transparent;
  color: var(--preto);
}
</style>
