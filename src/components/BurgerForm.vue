<template>
  <div>
    <p>Componente de mensagem</p>
    <div id="form-container">
      <form id="burger-form">

        <div class="input-container">
          <label for="name">Nome do Cliente</label>
          <input type="text" id="name" name="name" v-model="name" placeholder="Digite o seu nome">
        </div>
        <div class="input-container">
          <label for="bread">Escolha o Pão do seu Burger:</label>
          <select name="bread" id="bread" v-model="bread">
            <option value="" selected>Escolha seu pão</option>
          </select>
        </div>
        <div class="input-container">
          <label for="beef">Escolha sua Carne do seu Burger:</label>
          <select name="beef" id="beef" v-model="beef">
            <option value="" selected>Escolha sua Carne</option>
          </select>
        </div>
        <div class="input-container">
          <label for="optionals">Escolha os opcionais:</label>
          <div class="checkbox-container">
            <input type="checkbox" id="optionals" name="optionals" v-model="optionals" value="salame">
            <span>salame</span>
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

export default{
  name: "BurgerForm"
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
