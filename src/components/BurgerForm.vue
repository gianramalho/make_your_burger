<template>
  <div>
    <Message :msg="msg" v-show="msg" />
    <div id="form-container">
      <form id="burger-form" @submit="createBurger">

        <div class="input-container">
          <label for="name">Nome do Cliente</label>
          <input type="text" id="name" name="name" v-model="name" placeholder="Digite o seu nome">
        </div>
        <div class="input-container">
          <label for="bread">Escolha o Pão do seu Burger:</label>
          <select name="bread" id="bread" v-model="bread">
            <option value="">Escolha seu pão</option>
            <option v-for="bread in breads" :key="bread.id" :value="bread.tipo">{{ bread.tipo }}</option>
          </select>
        </div>
        <div class="input-container">
          <label for="beef">Escolha sua Carne do seu Burger:</label>
          <select name="beef" id="beef" v-model="beef">
            <option value="">Escolha sua Carne</option>
            <option v-for="beef in beefs" :key="beef.id" :value="beef.tipo">{{ beef.tipo }}</option>
          </select>
        </div>
        <div class="input-container">
          <label for="optionals">Escolha os opcionais:</label>
          <div class="checkbox-container" v-for="optional in optionalsdata" :key="optional.id">
            <input type="checkbox" id="optionals" name="optionals" v-model="optionals" :value="optional.tipo">
            <span>{{ optional.tipo }}</span>
          </div>
        </div>
        <div class="input-container">
          <input type="submit" class="submit-btn" value="Criar meu Burger">
        </div>

      </form>
    </div>
  </div>
  
</template>

<script>
import Message from "./Message.vue";

export default{
  name: "BurgerForm",
  data() {
    return {
      breads: null,
      beefs: null,
      optionalsdata: null,
      name: null,
      bread: null,
      beef: null,
      optionals: [],
      status: "Solicitado",
      msg: null
    }
  },
   methods: {
    async getIngredientes() {
      const req = await fetch('http://localhost:3000/ingredientes')
      const data = await req.json()
      this.breads = data.paes
      this.beefs = data.carnes
      this.optionalsdata = data.opcionais
    },
    async createBurger(e) {
      e.preventDefault()
      const data = {
        nome: this.name,
        carne: this.beef,
        pao: this.bread,
        opcionais: Array.from(this.optionals),
        status: "Solicitado"
      } 

      const dataJson = JSON.stringify(data)    

      const req = await fetch("http://localhost:3000/burgers", {
        method: "POST",
        headers: { "Content-Type" : "application/json" },
        body: dataJson
      });

      const res = await req.json()
      this.msg = "Pedido realizado com sucesso!"
      this.clearMsgInTime(3000)
      this.clearInputs()

    },
    clearInputs() {
      this.name = ""
      this.beef = ""
      this.bread = ""
      this.optionals = []
    },
    clearMsgInTime(timeInMs) {
      setTimeout(() => this.msg = "", timeInMs)
    },
  },
  mounted () {
    this.getIngredientes()
    this.clearInputs()
  },
  components: {
    Message,
  },
}
</script>

<style scoped>
  #form-container {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  #burger-form {
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
    color: #222;;
    padding: 5px 10px;
    border-left: 4px solid #fcba03;
  }
  input, select {
    padding: 5px 10px;
    width: 300px;
  }
  #opcionais-container {
    flex-direction: row;
    flex-wrap: wrap;
  }
  #opcionais-title {
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
    font-weight: bold;
  }
  .submit-btn {
    background-color: #222;
    color:#fcba03;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
  }
  .submit-btn:hover {
    background-color: transparent;
    color: #222;
  }
</style>
