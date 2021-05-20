<template>
  <div class="calculator">
    <div class="display"><div class="current">{{current || 0}}</div></div>
    <button class="operator2" @click="clear">C</button>
    <button class="operator2" @click="sign">+/-</button>
    <button class="operator2">%</button>
    <button class="operator">÷</button>
    <button>7</button>
    <button>8</button>
    <button>9</button>
    <button class="operator">x</button>
    <button>4</button>
    <button>5</button>
    <button>6</button>
    <button class="operator">-</button>
    <button>1</button>
    <button>2</button>
    <button>3</button>
    <button class="operator">+</button>
    <button class="zero">0</button>
    <button>.</button>
    <button class="operator">=</button>
  </div>
</template>

<script>
export default {

  data() {
    return {
      current: '',
    }
  },
  methods: {
    clear() {
      this.current = '';
    },
    sign() {
      this.current = this.current.charAt(0) === '-' ? this.current.slice(1) : `- ${this.current}`;
    }
    
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
