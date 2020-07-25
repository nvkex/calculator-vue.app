<template>
  <main class="calculator">
    <div class="display">
      000
    </div>
    <div class="buttons">
      <div
        class="button-row"
        v-for="(row, index) in buttonRows"
        v-bind:key="{ index }"
      >
        <div
          :class="{ operator: button.type == 'operator', special: button.type == 'special' }"
          class="button"
          v-for="(button, index) in row"
          v-bind:key="{ index }"
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
  data: () => ({
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
          text: "C",
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
          text: "*",
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
          type: "special",
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
          type: "operator",
        },
      ],
    ],
  }),
};
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

.display{
  text-align: right;
  font-size: 48px;
  padding: 30px;
}

.calculator {
  overflow:hidden;
  min-width: 250px;
  opacity: 0.9;
  box-shadow: 0px 0px 20px 8px rgba(0, 0, 0, 0.24);
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

.button:hover{
  background: rgb(85, 85, 85);
}

.button:active{
  background: rgb(116, 116, 116);
}

.operator {
  background: rgba(22, 22, 22, 0.89);
}

.special {
  background: rgba(22, 22, 22, 0.89);
}

</style>
