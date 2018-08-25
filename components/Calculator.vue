<template>
  <div class="calculator">

    <div class="display">{{current || '0'}}</div> // output number zero - if its not defined
    <div @click="clear" class="btn">AC</div>
    <div @click="sign" class="btn">+/-</div>
    <div @click="percent" class="btn">%</div>
    <div @click="divide" class="btn operator">÷</div>
    <div @click="append('7')" class="btn">7</div>  // using APPEND method to show the string with number
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div @click="times" class="btn operator">x</div>
    <div @click="append('4')" class="btn">4</div>
    <div @click="append('5')" class="btn">5</div>
    <div @click="append('6')" class="btn">6</div>
    <div @click="subtract" class="btn operator">-</div>
    <div @click="append('1')" class="btn">1</div>
    <div @click="append('2')" class="btn">2</div>
    <div @click="append('3')" class="btn">3</div>
    <div @click="add" class="btn operator">+</div>
    <div @click="append('0')" class="btn zero">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equal" class="btn operator">=</div>

  </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      current: '',  // renderring current data
      operator: null,
      operatorClicked: false,  // boolean operator
    }
  },
  methods: {
    clear() {
      this.current = '';  // define CLEAR method
    },
    sign() {
      this.current = this.current.charAt(0) === '-' ?
        this.current.slice(1) : `-${this.current}`;
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`;  //callback function
    },
    append(number) {    // implementing numbers and taking them as an argument
      if (this.operatorClicked) {
        this.current = '';
        this.operatorClicked = false;  // setting back to empty state
      }
      this.current = `${this.current}${number}`;  // joining to strings togheter
    },
    dot() {
      if (this.current.indexOf('.') === -1) {  // making sure that dot doesn't append twise
        this.append('.');
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    times() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    subtract() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    add() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    equal() {  // run that operator against previous and the current
      this.current = `${this.operator(
        parseFloat(this.current),
        parseFloat(this.previous)
      )}`;
      this.previous = null;  // resetting previous
    }
  }
}
</script>

<style scoped>
.calculator {
  margin: 0 auto;
  width: 600px;
  font-size: 50px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);  // 4 equal rows
  grid-auto-rows: minmax(100px, auto);
}
.display {
  grid-column: 1 / 5;  // column take entire first row
  background-color: #4fc08d;
  color: white;
}
.zero {
  grid-column: 1 / 3;
}
.btn {
  background-color: #F2F2F2;
  border: 1px solid #999;
}
.operator {
  background-color: #34495e;
  color: white;
}
</style>
