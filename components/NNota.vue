<template>
  <div class="card bg-warning my-5">
    <div class="card-body">
      <b-form @submit.prevent="adicionar" autocomplete="off">
        <b-form-group>
          <b-form-input
            class="border-0 text-dark"
            v-model="nota.titulo"
            type="text"
            placeholder="Titulo"
            size="lg"
          ></b-form-input>
        </b-form-group>
        <b-form-group>
          <b-form-textarea
            class="text-dark"
            v-model="nota.descricao"
            type="text"
            placeholder="Descrição"
            rows="10"
            size="lg"
            :autofocus="true"
            :required="true"
          ></b-form-textarea>
        </b-form-group>

        <ul class="list-unstyled">
          <li v-for="(item, index) of nota.checklists" :key="index">
            <b-input-group class="mb-2">
              <n-checklist
                :concluida="nota.checklists[index]['concluida']"
                :descricao="nota.checklists[index]['descricao']"
              ></n-checklist>
            </b-input-group>
          </li>
          <li>
            <n-checklist
              :concluida="checklist.concluida"
              :descricao="checklist.descricao"
            ></n-checklist>
          </li>
        </ul>


        <b-input-group>
          <b-form-tags
            input-id="tags-basic"
            v-model="nota.tags"
            placeholder="Adicione tags"
          ></b-form-tags>
        </b-input-group>


        <b-button type="button" variant="warning">
          <b-icon icon="check2-square" />
        </b-button>
        <b-button type="button" variant="warning">
          <b-icon icon="tag" />
        </b-button>
        <b-button type="submit" variant="dark">
          Adicionar
        </b-button>

      </b-form>
    </div>
  </div>
</template>

<script>
export default {
  name: "n-nota",
  props: {
    id: Number
  },
  data () {
    return {
      nota: {
        titulo: null,
        descricao: null
        //checklists: [
        //  {
        //    descricao: "Teste 1",
        //    concluida: 1
        //  }
        //],
        //tags: ["Tag 1", "Tag 2"]
      },
      checklist: {
        descricao: null,
        concluida: 0
      }
    };
  },
  computed: {
    notas() {
      return this.$store.state.nota.list;
    }
  },
  methods: {
    async adicionar() {
      const notaSaved = await this.$store.dispatch("nota/add", this.nota);

      this.$router.push(`/nota/edit/${notaSaved.id}`);
    },
    async carregar(){
      const { data } = await this.$axios.get(`nota/${this.id}`);
      this.nota = data;
    }
  },
  async mounted() {
    if(this.id) {
      await this.carregar();
    }
  }
};

</script>

<style scoped>

</style>
