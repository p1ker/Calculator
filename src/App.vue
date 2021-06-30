<template>
  <div id="app">
    <h1 class="calcul-ator">  Calcul - ator INT </h1>
    <div class="calculator">
      <div class="result">
        <input class="input" type="text" v-model="result">
      </div>
      <div class="buttons">
        <div class="numbers">
          <button  class="number" v-for="(number, index) in numbers" :key="index" v-on:click="input(number)">{{ number }}</button>
          <button class="ravno" v-on:click="calc()">=</button>
          <button class="C" v-on:click="clear()">C</button>
        </div>
        <div class="operations">
          <button class="operation" v-for="(operation, index) in operations" :key="index" v-on:click="input(operation)">{{ operation }}</button>
        </div>
      </div>
      <div class="res-buttons">

      </div>
    </div>

  </div>

</template>

<script>

import '@/assets/global.css';

export default {
  name: 'app',
  data: function () {
    return {
      result: '0',
      numbers: [ '1', '2', '3', '4','5', '6', '7', '8', '9', '0'],
      operations: [ '+', '-', '*', '/'],
      flag: false
    }
  },
  methods: {
    input: function(symbol){
      if (this.flag){
        this.clear()
      }
      if (this.numbers.includes(symbol) && this.result === '0') {
        return (this.result = symbol)
      }
      if (this.operations.includes(symbol) && this.operations.includes(this.result.slice(-1))) {
        this.result = this.result.slice(0,-1) + symbol
      }
      else  {
        if (this.operations.includes(symbol)){
          this.result = this.result + ' ' + symbol + ' '
        }
        else {
          this.result = this.result + symbol
        }
      }
    },

    calc: function(){
      this.result = eval(this.result)
      this.flag = true
    },

    clear: function (){
      this.result = '0'
      this.flag = false
    }
  }
}
</script>

<style>
#app {
  display:flex;
  flex-direction: column;
  align-items:center;
  color: #2c3e50;
  width: 100%;
  min-height: 100vh;
  background-repeat: no-repeat ;
  background-size: cover;
  background-image: url("https://marketingland.com/wp-content/ml-loads/2014/08/data-numbers-ss-1920.jpg");
}

.numbers {
  margin-top: 10px;
  width: 400px;
  display: grid;
  grid-gap: 3px;
  grid-template-columns: 1fr 1fr 1fr;
}

.result {
  display: flex;
  flex-direction: column;
}

.zero {
  grid-column-start: 2;
}



.buttons {
  display: flex;

}

.operations {
  display: flex;
  flex-direction: column;
  margin-left: 10px;
  margin-top: 10px;
  grid-gap: 3px;
}
.operation {
  background-color: chocolate;
  color: white;
  font-size: 28px;
  height: 75px;
  width: 75px;
  border-radius: 5px;
}
.calculator {
  margin-top: 10px;
  background-color: rgba(0, 125, 215, 0.5);
  padding: 10px;
}

.number {
  background-color: blueviolet;
  font-size: 28px;
  color: white;
  height: 75px;
  border-radius: 5px;
  border-color: indigo;
}

.input {
  height:75px;
  font-size: 28px;
  text-align: right;
  width: 393px;
  border-radius: 5px;
}

.res-buttons {
  display: grid;
  grid-template-columns: 1fr 1fr ;

}

.calcul-ator {
  background-color: rgba(0, 0, 0, 0.8);
  font-size: 100px;
  color: white;
  padding: 10px;
  border-radius: 40px;
}

.ravno {
  background-color: green;
  border-radius: 5px;
  font-size: 28px;
  color:white;
}

.C {
  background-color: red;
  border-radius: 5px;
  font-size: 28px;
  color:white;
}
</style>
