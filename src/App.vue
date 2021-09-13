<template>
  <div class="h-screen w-screen flex flex-col justify-center items-center bg-green-50">
    <div class="bg-green-300 border-green-600 border-b p-6 m-4 rounded">
      <h1 class="text-center w-full font-bold text-3xl text-gray-600 p-4">Busque por um CEP</h1>
      <div class="w-full bg-gray-400 my-3" style="height: 1px"></div>
      <form @submit.prevent="cepSearch(cep)">
        <div class="flex flex-col gap-4 px-0 py-4">
          <input
            class="text-center self-center py-2  border border-gray-200 w-min"
            pattern="[0-9]+"
            title="Por favor, insira um CEP válido"
            required="required"
            type="text"
            placeholder="Digite o CEP desejado"
            v-model="cep"
          />
          <button
            class=" m-4 bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 border border-blue-700 rounded w-min self-center"
          >
            Buscar
          </button>
        </div>
      </form>
      <div class=" w-max ">
        <Results v-if="results && !errorMessage" :results="results" />
        <p v-if="errorMessage">{{ errorMessage }}</p>
      </div>
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
      errorMessage: '',
    };
  },
  methods: {
    async cepSearch(cep) {
      const res = await fetch('https://cep.awesomeapi.com.br/json/' + cep);
      const data = await res.json();

      if (data.status) {
        if (data.status === 404) {
          this.errorMessage = data.message;
        }
        if (data.status === 400) {
          this.errorMessage = data.message;
        }
      } else {
        this.results = data;
        this.errorMessage = '';
      }
    },
  },
};
</script>

<style></style>
