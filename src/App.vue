<template>
 <div class="calculator">
  <div class="display">{{calculatorValue || 0}}</div>
    <div class="row">
     
    <div class="sign" @click="clear">C</div>
    <div class="sign" @click="multiply" >*</div>
    <div class="sign" @click="divide">/</div>
    <div class="sign" @click="minus">-</div>
    <div @click="append('7')" >7</div>
    <div @click="append('8')">8</div>
    <div @click="append('9')">9</div>
    <div class="sign" @click="Add">+</div>
    <div @click="append('4')">4</div>
    <div @click="append('5')">5</div>
    <div @click="append('6')">6</div>
    <div class="sign" @click="percent">%</div>
    <div @click="append('1')">1</div>
    <div @click="append('2')">2</div>
    <div @click="append('3')">3</div>
    <div class="sign" @click="equal">=</div>
    <div @click="append('0')">0</div>
    <div @click="point()" >.</div>
    <div @click="sign">+/-</div>
    <div class="sign" @click="del" >Del</div>
    </div>

 </div>

</template>

<script>


export default {
  name: 'App',
  components: {
   
  },
  data(){
    return{
      previousValue: null,
      calculatorValue:'',
      operator:null,
      operationClicked : false

    }
  },
  methods:{
    append(number){
      if(this.operationClicked){
        this.calculatorValue = ''
        this.operationClicked = false
      }
      this.calculatorValue = `${this.calculatorValue}${number}`
    },
    point(){
      if(this.calculatorValue.indexOf('.') === -1 ) {
        this.append('.')
  
      
    }
  },
    del(){
      this.calculatorValue = this.calculatorValue.slice(0, -1)
    },
    clear(){
      this.calculatorValue = ''
    },
    setPrevious(){
      this.previousValue = this.calculatorValue
      this.operationClicked = true
    },
    Add(){
      this.operator = (a,b) => a + b
      this.setPrevious()
    },
    multiply(){
      this.operator = (a,b) => a * b
      this.setPrevious()
    },
    divide(){
      this.operator = (a,b) => a * b
      this.setPrevious()
    },
    minus(){
      this.operator = (a,b) => a * b
      this.setPrevious()
    },
    sign(){
      this.calculatorValue = this.calculatorValue.charAt(0) === ('-') ?
      this.calculatorValue.slice(1) : `-${this.calculatorValue}`
    },
    equal(){
      this.calculatorValue = `${this.operator(parseFloat(this.calculatorValue),
        parseFloat(this.previousValue))}`
    },
    percent(){
      this.calculatorValue = parseFloat(this.calculatorValue) / 100
    }

  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

@media screen and (max-width : 600px) {
  #app{
    margin-top: 100px ;
  }
}

@media screen and (max-width : 400px) {
  #app{
    margin-top: 60px ;
  }
}

</style>
