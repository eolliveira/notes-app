<template>
  <b-input-group class="mb-2">
    <b-input-group-prepend is-text>
      <b-form-checkbox
        :value="1"
        :unchecked-value="0"
        class="mr-n2"
        v-model="concluida"
      />
    </b-input-group-prepend>
    <b-form-input
      placeholder="Novo Item"
      class="text-dark border-0"
      :class="{ 'concluida': concluida == 1 }"
      v-model="descricao"
    />
  </b-input-group>
</template>

<script>
export default {
  name: "n-checklist",
  props: {
    concluida: {
      type: [Number, Boolean ],
      default: 0,
      require: true
    },
    descricao: {
      type: String,
      default: null
    }
  }
};
</script>

<style scoped>
.concluida {
  text-decoration: line-through;
}
</style>

