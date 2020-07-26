<template>
  <main class="calculator">
    <div class="prev-display">
      {{ previousValue }}
    </div>
    <div class="display">
      {{ display }}
    </div>
    <div class="buttons">
      <div
        class="button-row"
        v-for="(row, index) in buttonRows"
        v-bind:key="index"
      >
        <div
          @click="buttonClick(button)"
          :class="{
            operator: button.type == 'operator',
            special: button.type == 'special',
            equal: button.type == 'equal',
          }"
          class="button"
          v-for="(button, index) in row"
          v-bind:key="index"
        >
          {{ button.text }}
        </div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  name: "App",
  methods: {
    evaluate(button) {
      this.previousValue += this.display;
      this.fullExpr += this.display;
      this.fullExpr = this.fullExpr.replace(/×/g, "*");
      this.fullExpr = this.fullExpr.replace(/÷/g, "/");

      let res = eval(this.fullExpr);
      this.display = res;

      this.fullExpr = this.fullExpr.replace(/\*/g, "×");
      this.fullExpr = this.fullExpr.replace(/\//g, "÷");
      this.currentOperator = button.text;
    },
    buttonClick(button) {
      if (button.type == "number") {
        if (this.display == "0") this.display = button.text;
        else this.display += button.text;
        if (this.currentOperator != "") {
          this.display = button.text;
          this.currentOperator = "";
        }
      } 
      else if (button.text == "CE") {
        this.display = "0";
        this.previousValue = "";
        this.fullExpr = "";
      } 
      else if (button.text == "+/-") {
        this.display *= -1;
      } 
      else if (button.text == "←") {
        if (parseInt(this.display) > "9")
          this.display = this.display.slice(0, this.display.length - 1);
        else this.display = "0";
      } 
      else if (button.text == "=") {
        this.evaluate(button);
      } 
      else if (button.type == "operator") {
        if (this.currentOperator == "=") {
          this.previousValue += button.text;
        } else {
          this.previousValue += this.display + button.text;
          this.currentOperator = button.text;
          this.fullExpr =
            "(" + this.fullExpr + this.display + ")" + button.text;
        }
      }
    },
  },
  data: () => ({
    display: "0",
    previousValue: "",
    currentOperator: "",
    fullExpr: "",
    buttonRows: [
      [
        {
          text: "%",
          type: "operator",
        },
        {
          text: "CE",
          type: "special",
        },
        {
          text: "←",
          type: "special",
        },
        {
          text: "÷",
          type: "operator",
        },
      ],
      [
        {
          text: "7",
          type: "number",
        },
        {
          text: "8",
          type: "number",
        },
        {
          text: "9",
          type: "number",
        },
        {
          text: "×",
          type: "operator",
        },
      ],
      [
        {
          text: "4",
          type: "number",
        },
        {
          text: "5",
          type: "number",
        },
        {
          text: "6",
          type: "number",
        },
        {
          text: "-",
          type: "operator",
        },
      ],
      [
        {
          text: "1",
          type: "number",
        },
        {
          text: "2",
          type: "number",
        },
        {
          text: "3",
          type: "number",
        },
        {
          text: "+",
          type: "operator",
        },
      ],
      [
        {
          text: "+/-",
          type: "abs",
        },
        {
          text: "0",
          type: "number",
        },
        {
          text: ".",
          type: "number",
        },
        {
          text: "=",
          type: "equal",
        },
      ],
    ],
  }),
};
</script>

<style>
body {
  overflow: hidden;
  /* background-repeat: no-repeat;
  background: url('./assets/lgKPRvT.jpg'), rgba(0, 0, 0, 0.6);
  background-blend-mode: overlay; */
  background: linear-gradient(#8cdbdb, #ffcccc);
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100vw;
  height: 100vh;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.prev-display {
  overflow: auto;
  color: grey;
  text-align: right;
  font-size: 20px;
  padding: 10px 30px;
}

.display {
  overflow: auto;
  text-align: right;
  font-size: 48px;
  padding: 30px;
}

.calculator {
  overflow: hidden;
  min-width: 250px;
  opacity: 0.95;
  box-shadow: 0px 0px 20px 4px rgba(0, 0, 0, 0.2);
  color: white;
  width: 40%;
  background: rgb(39, 39, 39);
  padding: 4px;
}

.buttons {
  text-align: center;
}

.button-row {
  display: flex;
  justify-content: space-around;
}

.button {
  cursor: pointer;
  background: rgba(0, 0, 0, 0.959);
  color: white;
  width: 100%;
  display: inline-block;
  outline: 2px solid rgb(39, 39, 39);
  padding: 16px 20px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.button:hover {
  background: rgb(85, 85, 85);
}

.button:active {
  background: rgb(116, 116, 116);
}

.operator {
  background: rgba(22, 22, 22, 0.89);
}

.special {
  background: rgba(22, 22, 22, 0.89);
}

.equal {
  background: rgba(66, 66, 66, 0.815);
}
</style>
