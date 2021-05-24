<template>
  <div class="background" :class="{ darkMode: darkMode }">
    <div>
      <input type="checkbox" class="checkbox" id="chk" @click="toggle" />
      <label class="label" for="chk">
        <div class="ball" :class="{ darkMode: darkMode }"></div>
      </label>
    </div>
    <div class="calculator-container">
      <div class="calculator">
        <div class="display" :class="{ darkMode: darkMode }">
          <div class="current" :style="'font-size:' + fontSize + '%'">
            {{ current || "0" }}
          </div>
        </div>
        <button
          class="operator2"
          :class="{ darkMode: darkMode }"
          @click="clear"
        >
          C
        </button>
        <button class="operator2" :class="{ darkMode: darkMode }" @click="sign">
          +/-
        </button>
        <button
          class="operator2"
          :class="{ darkMode: darkMode }"
          @click="percent"
        >
          %
        </button>
        <button
          class="operator"
          :class="{ darkMode: darkMode }"
          @click="divide"
        >
          ÷
        </button>
        <button :class="{ darkMode: darkMode }" @click="append('7')">7</button>
        <button :class="{ darkMode: darkMode }" @click="append('8')">8</button>
        <button :class="{ darkMode: darkMode }" @click="append('9')">9</button>
        <button class="operator" :class="{ darkMode: darkMode }" @click="times">
          x
        </button>
        <button :class="{ darkMode: darkMode }" @click="append('4')">4</button>
        <button :class="{ darkMode: darkMode }" @click="append('5')">5</button>
        <button :class="{ darkMode: darkMode }" @click="append('6')">6</button>
        <button class="operator" :class="{ darkMode: darkMode }" @click="minus">
          -
        </button>
        <button :class="{ darkMode: darkMode }" @click="append('1')">1</button>
        <button :class="{ darkMode: darkMode }" @click="append('2')">2</button>
        <button :class="{ darkMode: darkMode }" @click="append('3')">3</button>
        <button class="operator" :class="{ darkMode: darkMode }" @click="plus">
          +
        </button>
        <button
          :class="{ darkMode: darkMode }"
          class="zero"
          @click="append('0')"
        >
          0
        </button>
        <button :class="{ darkMode: darkMode }" @click="dot">.</button>
        <button class="operator" :class="{ darkMode: darkMode }" @click="equal">
          =
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentString: "",
      current: "",
      operator: null,
      operators: [],
      operatorClicked: false,
      darkMode: false,
    };
  },
  computed: {
    fontSize() {
      if (this.current.length >= 10 && this.current.length < 20) {
        return 250 - this.current.length ** 1.57;
      }
      if (this.current.length >= 20) {
        return 250 - this.current.length * 5.5;
      }
      return 250;
    },
  },
  methods: {
    clear() {
      this.current = "";
      this.previous = null;
      this.operators = [];
    },
    sign() {
      if (this.current !== "") {
        this.current =
          this.current.charAt(0) === "-"
            ? this.current.slice(1)
            : `-${this.current}`;
      }
    },
    percent() {
      if (this.current !== null)
        this.current = `${parseFloat(this.current) / 100}`;
    },
    append(number) {
      if (this.operatorClicked) {
        this.current = "";
        this.operatorClicked = false;
      }
      //preventing to append if number is result of operation
      if (this.operators.length === 0) {
        //max lenght 25
        if (this.current.length >= 25) {
          return this.current;
        }
        if (this.current === "" || this.current === "0") {
          this.current = number;
        } else {
          this.current = `${this.current}${number}`;
        }
      }
    },
    dot() {
      if (this.current.indexOf(".") === -1) this.append(".");
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide() {
      this.operators = [];
      this.operator = (a, b) => Math.round((a / b) * 10000) / 10000;
      this.setPrevious();
    },
    times() {
      this.operators = [];
      this.operator = (a, b) => Math.round(a * b * 10000) / 10000;
      this.setPrevious();
    },
    minus() {
      this.operators = [];
      this.operator = (a, b) => Math.round((a - b) * 10000) / 10000;
      this.setPrevious();
    },
    plus() {
      this.operators = [];
      this.operator = (a, b) => Math.round((a + b) * 10000) / 10000;
      this.setPrevious();
    },
    equal() {
      if (this.previous) {
        this.operators.push(this.operator);
        this.current = `${this.operator(
          parseFloat(this.previous),
          parseFloat(this.current)
        )}`;
      }
      this.previous = null;

      console.log("operators", this.operators.length);
    },
    toggle() {
      this.darkMode ? (this.darkMode = false) : (this.darkMode = true);
    },
  },
};
</script>

<style scoped>

/* Mobile Styles */
.background {
  min-height: 100%;
  background-color: #eeeeee;
  transition: 0.3s ease-in-out;
}
.darkMode {
  background-color: #090c10;
  color: #222831 !important;
}
.calculator-container {
  margin-top: 15%;
}
.calculator {
  text-align: center;
  margin: 5% auto;
  display: grid;
  width: 48vh;
  padding: 0;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(7vh, 9vh);
  box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
}
.display {
  display: grid;
  grid-column: 1 / 5;
  grid-row: 1 / 3;

  background: radial-gradient(#1a4652 1%, transparent 5%) 0 0,
    radial-gradient(#1a4652 1%, transparent 5%) 8px 8px,
    radial-gradient(rgba(246, 245, 245, 0.1) 15%, transparent 20%) 0 1px,
    radial-gradient(rgba(246, 245, 245, 0.1) 15%, transparent 20%) 8px 9px;
  background-color: #276678;
  background-size: 16px 16px;
  color: #d3e0ea;
  transition: 0.3s ease-in-out;
}
.current {
  align-self: center;
  justify-self: right;
  padding-right: 8%;
  font-size: 3em;
  overflow: hidden;
}
.zero {
  grid-column: 1 / 3;
}
button {
  font-size: 0.9em;
  background-color: #d3e0ea;
  border: 1px solid rgba(246, 245, 245, 0.5);
  transition: 0.3s ease-in-out;
}
button.darkMode {
  background-color: #393e46;
  color: #d3e0ea !important;
  border: 1px solid #222831 !important;
}
.operator {
  background-color: #1687a7;
  transition: 0.3s ease-in-out;
}
.operator.darkMode {
  background-color: #222831;
  color: #d3e0ea !important;
}
.operator2 {
  background-color: #f6f5f5;
  transition: 0.3s ease-in-out;
}
.operator2.darkMode {
  background-color: #222831;
  color: #d3e0ea !important;
}
/* toggle */
.checkbox {
  opacity: 0;
}
.label {
  background-color: #276678;
  box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
  border-radius: 50px;
  margin-left: 5%;
  margin-top: 4%;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 5px;
  position: relative;
  height: 4vw;
  width: 7vw;
  transform: scale(1.5);
}
.label .ball {
  background-color: #f6f5f5;
  box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
  border-radius: 50%;
  height: 3vw;
  width: 3vw;
  transform: translateX(0px);
  transition: 0.3s ease-in-out;
}
.checkbox:checked + .label .ball {
  transform: translateX(150%);
}
.ball.darkMode {
  background-color: #d3e0ea;
}
/* Tablet Styles */
@media only screen and (min-width: 768px) {
  .label {
    height: 2vw;
    width: 5vw;
  }
  .label .ball {
    height: 2vw;
    width: 2vw;
  }
}

/* Desktop styles */
@media only screen and (min-width: 1080px) {
  .calculator {
    width: 40vh;
    grid-auto-rows: minmax(7vh, 8vh);
  }
  .calculator-container {
    margin-top: 0%;
  }
  .label {
    margin-top: 0;
    height: 1vw;
    width: 3vw;
  }
  .label .ball {
    height: 1vw;
    width: 1vw;
  }
  .checkbox:checked + .label .ball {
    transform: translateX(200%);
  }
}
</style>
