<template>
  <b-input-group>
    <b-form-tags
      class="bg-warning border-0 text-dark"
      tag-variant="dark"
      placeholder="Adicione tags"
      v-model="descricao"
    >
    </b-form-tags>
  </b-input-group>
</template>

<script>
export default {
  name: "n-tag",
  props: {
    descricao: {
      type: [String, Array],
      default: null,
      required: true
    }
  }
}
</script>

<style scoped>

</style>
