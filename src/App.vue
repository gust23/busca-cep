<template>
  <div class="flex h-screen justify-center items-center bg-green-50">
    <div class="text-center">
      <h1 class="text-3xl">Busque por um CEP</h1>
      <form @submit.prevent="cepSearch(text)">
        <input pattern="[0-9]+" title="Porfavor, insira um CEP válido" required="required" type="text" v-model="cep" />
        <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 border border-blue-700 rounded">
          Button
        </button>
      </form>

      <Results v-if="results" :results="results" />
    </div>
  </div>
</template>

<script>
import Results from './components/Results.vue';
export default {
  name: 'App',
  components: { Results },
  data() {
    return {
      cep: '',
      results: null,
    };
  },
  methods: {
    async cepSearch(cep) {
      const res = await fetch('https://cep.awesomeapi.com.br/json' + cep);
      const data = await res.json();
      this.results = data;
      console.log(this.results);
    },
  },
};
</script>

<style></style>
