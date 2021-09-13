<template lang="">
  <div>
    <div>
      <h2>Resutado da busca:</h2>
      <p>Logradouro: {{ results.address }}</p>
      <p>Bairro: {{ results.district }}</p>
      <p>Localização: {{ results.city }} {{ results.state }}</p>
      <p>Código de Área: {{ results.ddd }}</p>
    </div>
  </div>
</template>
<script>
export default {
  props: ['results'],
};
</script>
<style lang=""></style>
