<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-md-7 d-flex vh-100 justify-content-center">
        <div class="col-md-5 align-self-center">
          <h1 class="text-center mb-5">Notes App</h1>
          <p>Informe seus Dados: </p>

          <b-form @submit.prevent="cadastrar">

            <b-form-group>
              <b-form-input
                v-model="nome"
                type="text"
                placeholder="Nome"
                required
              ></b-form-input>
            </b-form-group>

            <b-form-group>
              <b-form-input
                v-model="email"
                type="email"
                placeholder="E-mail"
                required
              ></b-form-input>
            </b-form-group>

            <b-form-group>
              <b-form-input
                v-model="senha"
                type="password"
                placeholder="Senha"
                required
              ></b-form-input>
            </b-form-group>

            <b-button block type="submit" variant="primary">Cadastrar</b-button>
          </b-form>
        </div>
      </div>
      <div class="col-md-5 vh-100 cover"></div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      nome: null,
      email: null,
      senha: null
    }
  },
  methods: {
    async cadastrar() {
      try {
        let data = {
          nome: this.nome,
          email: this.email,
          senha: this.senha
        };

        await this.$axios.post(`registro`, data);


        this.$router.push("/");
      } catch (e) {
        console.log(e);
      }
    }
  }
};
</script>

<style>
  .cover {
   background: url("https://url.gratis/wftZc") center center;
  }
</style>
