<template>
  <div>
    <Message :msg="msg" v-show="msg" />
    <div>
      <form @submit="createChurro($event)" id="churro-form">
        <div class="input-container">
          <label for="nome">Nome do Cliente</label>
          <input type="text" id="nome" name="name" v-model="nome" placeholder="Digite seu nome"/>
        </div>

        <div class="input-container">
          <label for="recheio">Escolha o Recheio:</label>
          <select name="recheio" id="recheio" v-model="recheio">
            <option value="">Selecione seu recheio</option>
            <option v-for="recheio in recheios" :key="recheio.id" :value="recheio.tipo">
              {{ recheio.tipo }}
            </option>
          </select>
        </div>

        <div class="input-container">
          <label for="cobertura">Escolha a Cobertura:</label>
          <select name="cobertura" id="cobertura" v-model="cobertura">
            <option value="">Selecione sua cobertura</option>
            <option v-for="cobertura in coberturas"  :key="cobertura.id"  :value="cobertura.tipo">
              {{ cobertura.tipo }}
            </option>
          </select>
        </div>

        <div class="input-container">
          <label for="acompanhamento">Escolha o acompanhamento seco</label>
          <select  name="acompanhamento"  id="acompanhamento"  v-model="acompanhamento">
            <option value="">Selecione seu acompanhamento:</option>
            <option v-for="acompanhamento in acompanhamentos"  :key="acompanhamento.id"  :value="acompanhamento.tipo">
              {{ acompanhamento.tipo }}
            </option>
          </select>
        </div>

        <div id="adicionais-container" class="input-container">
          <label id="adicionais-title" for="adicionais">Escolha os adicionais:</label >
          <div  class="checkbox-container" v-for="adicionais in adicionaisdata" :key="adicionais.id"   >
            <input  type="checkbox"  name="adicionais" v-model="adicionais.tipo" :value="adicionais.tipo">
            <span>{{ adicionais.tipo }} </span>
          </div>
        </div>

        <div class="input-container">
          <input type="submit" class="submit-btn" value="Adicionar ao pedido" />
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import Message from "./Message.vue";
export default {
  name: "ChurroForm",
  data() {
    return {
      recheios: null,
      coberturas: null,
      acompanhamentos: null,
      adicionaisdata: null,
      nome: null,
      recheio: null,
      cobertura: null,
      acompanhamento: null,
      adicionais: [],
      msg: null,
    };
  },
  

  methods: {
    async getIngredientes() {

      const req = await fetch("http://localhost:3000/ingredientes");
      const data = await req.json();
      this.recheios = data.recheios;
      this.coberturas = data.coberturas;
      this.acompanhamentos = data.acompanhamentos;
      this.adicionaisdata = data.adicionais;
    },
    async createChurro(e) {
      e.preventDefault();
      //pegando o bd para renderizar seus dados na tela
      const data = {
        nome: this.nome,
        recheio: this.recheio,
        cobertura: this.cobertura,
        acompanhamento: this.acompanhamento,
        adicionais: Array.from(this.adicionais),
        status: "Solicitado",
      };

      const dataJson = JSON.stringify(data);

      //enviando os dados do form para o servidor
      const req = await fetch("http://localhost:3000/churros", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: dataJson,
      });

      const res = await req.json();
      //mns de sistema
      this.msg = `Pedido N°${res.id} realizado com sucesso`;
      //limpar mesagem
      setTimeout(() => (this.msg = ""), 3000);

      //limpar os campos
      this.nome = "";
      this.recheio = "";
      this.cobertura = "";
      this.acompanhamento = "";
      this.adicionais =[];
    },
  },
  mounted() {
    this.getIngredientes();
  },
  components: {
    Message,
  },
};
</script>

<style scoped>
#churro-form {
  max-width: 400px;
  margin: 0 auto;
}

.input-container {
  display: flex;
  flex-direction: column;
  margin-bottom: 20px;
}

label {
  font-weight: bold;
  margin-bottom: 15px;
  color: var(--preto);
  padding: 5px 10px;
  border-left: 4px solid var(--laranja);
}

input,
select {
  padding: 5px 10px;
  width: 300px;
}

#adicionais-container {
  flex-direction: row;
  flex-wrap: wrap;
}

#adicionais-title {
  width: 100%;
}

.checkbox-container {
  display: flex;
  align-items: flex-start;
  width: 50%;
  margin-bottom: 20px;
}

.checkbox-container span,
.checkbox-container input {
  width: auto;
}

.checkbox-container span {
  margin-left: 6px;
  font-weight: 600;
}

.submit-btn {
  background-color: var(--azul-escuro);
  color: var(--laranja);
  font-weight: bold;
  border: 2px solid var(--azul-escuro);
  padding: 10px;
  font-size: 16px;
  margin: 0 auto;
  transition: 0.5s;
  cursor: pointer;
}

.submit-btn:hover {
  background-color: transparent;
  color: var(--azul-escuro);
}
</style>
