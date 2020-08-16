<template>
  <div class="conversor">
    <h2>{{moedaA}} Para {{moedaB}}</h2>
    <input type="text" v-model="moedaA_valor" v-bind:placeholder="moedaA" />
    <input type="button" value="Converter" v-on:click="conversor" />
    <!-- Criando um botão para fazer a conversão e usando o v-on para criar um event listener que será ativado ao ser clicado e passado a função conversos como a ação a ser realizada  -->
    <h2>{{moedaB_valor}}</h2>
  </div>
</template>    

<script>
export default {
  name: "conversor",
  props: ["moedaA", "moedaB"],
  data() {
    return {
      moedaA_valor: "",
      moedaB_valor: 0,
    };
  },
  methods: {
    conversor() {
      let de_para = this.moedaA + "_" + this.moedaB;

      let url =
        "https://free.currconv.com/api/v7/convert?q=" +
        de_para +
        "&compact=ultra&apiKey=0ca8ebb495940c9d40db";
      // Usando uma API para converter as moedas

      fetch(url)
        //Fazendo uma requisição para a API
        .then(res => {
          return res.json();
        })
        // E então pegando o valor como um json
        .then(json => {
            console.log(json)
          let cotacao = json[de_para];
          this.moedaB_valor = (cotacao * parseFloat(this.moedaA_valor)).toFixed(
            2
          );
          // Atribuindo o valor do json a uma variável e então realizando a conta de conversão,
          // certificando-se que o valor passado é mesmo um float e mostrando somente duas casas decimais
        });
    }
  }
};
</script>

<style scoped>

.conversor{
max-width: 300px;
padding: 20px;
box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
    }

</style>