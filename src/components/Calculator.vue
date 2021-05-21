<template>
  <div class="calculator">
    <div class="display"><div class="current">{{current || 0}}</div></div>
    <button class="operator2" @click="clear">C</button>
    <button class="operator2" @click="sign">+/-</button>
    <button class="operator2" @click="percent">%</button>
    <button class="operator" @click="divide">÷</button>
    <button @click="append(7)">7</button>
    <button @click="append(8)">8</button>
    <button @click="append(9)">9</button>
    <button class="operator" @click="times">x</button>
    <button @click="append(4)">4</button>
    <button @click="append(5)">5</button>
    <button @click="append(6)">6</button>
    <button class="operator" @click="minus">-</button>
    <button @click="append(1)">1</button>
    <button @click="append(2)">2</button>
    <button @click="append(3)">3</button>
    <button class="operator" @click="plus">+</button>
    <button class="zero" @click="append(0)" >0</button>
    <button @click="dot">.</button>
    <button class="operator" @click="equal">=</button>
  </div>
</template>

<script>
export default {

  data() {
    return {
      previous: null,
      current: '',
      operator: null,
      operatorClicked: false
    }
  },
  methods: {
    clear() {
      this.current = '';
    },
    sign() {
      this.current = this.current.charAt(0) === '-' ? this.current.slice(1) : `- ${this.current}`;
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`
    },
    append(num) {
      if(this.operatorClicked) {
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${num}`;
    },
    dot() {
      if(this.current.indexOf('.') === -1) this.append('.');
    },
    setPrevious(){
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.setPrevious()
    },
    times() {
      this.operator = (a, b) => a * b;
      this.setPrevious()
    },
    minus() {
      this.operator = (a, b) => a - b;
      this.setPrevious()
    },
    plus() {
      this.operator = (a, b) => a + b;
      this.setPrevious()
    },
    equal() {
      this.current = `${this.operator(
        parseFloat(this.current),
        parseFloat(this.previous)
      )}`;
      this.previous = null;
    },      
  }
 
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}
.display {
  display: grid;
  grid-column: 1 / 5;
  grid-row: 1 / 3;
  
background:
radial-gradient(#1a4652 1%, transparent 5%) 0 0,
radial-gradient(#1a4652 1%, transparent 5%) 8px 8px,
radial-gradient(rgba(246, 245, 245,.1) 15%, transparent 20%) 0 1px,
radial-gradient(rgba(246, 245, 245,.1) 15%, transparent 20%) 8px 9px;
background-color:#276678;
background-size:16px 16px;
color: #d3e0ea; 
}

.current {
  align-self: center;
  justify-self:right;
  padding-right: 8% ;
  font-size: 3em;
}

.zero {
  grid-column: 1 / 3;
}
button {
  font-size: 0.8em;
  background-color: #d3e0ea;
  border: 1px solid rgba(246, 245, 245, 0.5);
}

.operator {
  background-color: #1687a7;
}
.operator2 {
  background-color: #f6f5f5;
}

</style>
