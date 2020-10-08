<template>
  <div class="calculator">
    <div class="display">{{ preNum }} {{ displayOperator }} {{ display }}</div>
    <div @click="clearBtn" class="button darker">C</div>
    <div @click="delOne" class="button darker">C^</div>
    <div @click="percentBtn" class="button darker">%</div>
    <div @click="divide" class="button operator">÷</div>
    <div @click="append(7)" class="button">7</div>
    <div @click="append(8)" class="button">8</div>
    <div @click="append(9)" class="button">9</div>
    <div @click="multiply" class="button operator">x</div>
    <div @click="append(4)" class="button">4</div>
    <div @click="append(5)" class="button">5</div>
    <div @click="append(6)" class="button">6</div>
    <div @click="minus" class="button operator">-</div>
    <div @click="append(1)" class="button">1</div>
    <div @click="append(2)" class="button">2</div>
    <div @click="append(3)" class="button">3</div>
    <div @click="plus" class="button operator">+</div>
    <div @click="append(0)" class="button zero button-bottom">0</div>
    <div @click="decimal" class="button darker button-bottom">.</div>
    <div @click="equalNum" class="button operator button-bottom">=</div>
  </div>
</template>

<script>
export default {
  name: "calculator",
  data() {
    return {
      preNum: null,
      display: 0,
      operator: null,
      operatorClicked: null,
      displayOperator: null,
    };
  },
  methods: {
    delOne() {
      if (this.displayOperator) {
        this.displayOperator = null;
      } else {
        this.display = this.display.slice(0, -1);
      }
    },
    clearBtn() {
      this.display = 0;
      this.preNum = null;
      this.displayOperator = null;
    },
    percentBtn() {
      this.display /= 100;
    },
    plus() {
      this.operator = (a, b) => a + b;
      this.preNum = this.display;
      this.operatorClicked = true;
      this.displayOperator = "+";
      this.display = "";
    },
    minus() {
      this.operator = (a, b) => a - b;
      this.preNum = this.display;
      this.operatorClicked = true;
      this.displayOperator = "-";
      this.display = "";
    },
    multiply() {
      this.operator = (a, b) => a * b;
      this.preNum = this.display;
      this.operatorClicked = true;
      this.displayOperator = "x";
      this.display = "";
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.preNum = this.display;
      this.operatorClicked = true;
      this.displayOperator = "/";
      this.display = "";
    },
    decimal() {
      if (this.display.indexOf(".") === -1) {
        this.append(".");
      }
    },
    equalNum() {
      this.display = this.operator(Number(this.preNum), Number(this.display));
      this.preNum = null;
      this.operatorClicked = true;
      this.displayOperator = null;
    },
    append(number) {
      if (this.operatorClicked === true) {
        this.display = "";
        this.operatorClicked = false;
      }
      if (this.display === 0) {
        this.display = number.toString();
      } else {
        this.display = "" + this.display + number.toString();
      }
    },
  },
};
</script>

<style>
.calculator {
  margin: 0 auto;
  width: 80vw;
  font-size: 2rem;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(10vh, auto);
  /* border: 5px solid #111; */
  box-shadow: -3px 3px 15px rgba(155, 129, 129, 0.4);
  line-height: 10vh;
}

.display {
  grid-column: 1 / 5;
  background:rgb(194, 250, 203);
  border-top: 0;
  font-size: 2.5rem;
  cursor: default;
  overflow: hidden;
  text-overflow: ellipsis;
  padding: 0 1rem;
}

.zero {
  grid-column: 1 / 3;
}

.button {
  background: rgb(255, 255, 255);
  
  border: black solid 1px;
  cursor:pointer;
}



.button-bottom {
  border-bottom: 0;
}

.operator {
  background: hsl(249, 68%, 30%);
  color: white;
}

.darker {
  background: hsl(352, 100%, 61%);
  /* background: linear-gradient(15deg, hsl(0, 0%, 60%) 0%, hsl(0, 0%, 70%) 100%); */
}
</style>