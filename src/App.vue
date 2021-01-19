<template>
  <v-app>
    <div class="main">
      <v-simple-table fixed-header>
      <template v-slot:default>
        <thead>
          <tr>
            <td>Название валюты</td>
            <td>Цена </td>
            <td>Количество</td>
          </tr>
        </thead>
        <tbody v-if="show">
          <tr v-for="currency in currencies" :key="currency.name">
            <td>{{currency.name}}</td>
            <td>{{Math.round(currency.volume)}}</td>
            <td>{{currency.price.amount.toFixed(2)}}</td>
          </tr>
        </tbody>
        <tbody v-else> 
          <tr>
            <td class="empty" colspan="3" loading>
              Нет данных
            </td>
          </tr>
        </tbody>
      </template>
    </v-simple-table>
  </div>
</v-app>
</template>

<script>

  export default {
    name: 'App',
    components: {
    },
    data: () => ({
     currencies: [],
     show: false
   }),
    mounted() {
      fetch('http://phisix-api3.appspot.com/stocks.json')
      .then(resp => resp.json())
      .then(data => { this.currencies = data.stock; this.show = true })
    }
  }
</script>

<style>
  .main{
    border: 1px solid #ccc;
    padding: 20px;
    width: 70%;
    margin: 30px auto;
    border-radius: 5px;
  }
  thead{
    color: rgba(0,0,0,.6);
  }
  thead td{
    font-size: 12px!important;
  }
  td{
    height: 50px!important;
  }
  .empty{
    text-align: center;
  }
</style>