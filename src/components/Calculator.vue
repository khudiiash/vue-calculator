<template>
  <div class="calculator">
    <div class="display">{{ current || 0 }}</div>
    <button @click="clear" class="btn operator">A/C</button>
    <button @click="sign" class="btn operator">+/-</button>
    <button @click="percent" class="btn operator">%</button>
    <button @click="append(`÷`)" class="btn operator">÷</button>
    <button @click="append(7)" class="btn">7</button>
    <button @click="append(8)" class="btn">8</button>
    <button @click="append(9)" class="btn">9</button>
    <button @click="append(`×`)" class="btn operator">×</button>
    <button @click="append(4)" class="btn">4</button>
    <button @click="append(5)" class="btn">5</button>
    <button @click="append(6)" class="btn">6</button>
    <button @click="append(`-`)" class="btn operator">-</button>
    <button @click="append(1)" class="btn">1</button>
    <button @click="append(2)" class="btn">2</button>
    <button @click="append(3)" class="btn">3</button>
    <button @click="append(`+`)" class="btn operator">+</button>
    <button @click="append(0)" class="btn zero">0</button>
    <button @click="append(`.`)" class="btn">.</button>
    <button @click="equals" class="btn operator equals">=</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      current: ""
    };
  },
  methods: {
    clear() {
      this.current = "";
    },
    sign() {
      this.current =
        this.current.charAt(0) === "-"
          ? this.current.slice(1)
          : `-${this.current}`;
    },
    percent() {
      this.current = `${this.current && this.current !== "-" ? parseFloat(this.current) / 100 : ""}`;
    },
    append(value) {
      if (this.current.length <= 12) {
        if (Number.isInteger(value) || value === ".") {
          this.current =
            this.current === "0" && value !== "." ? "" : this.current + value;
        } else if (this.current && !Number.isInteger(value) && this.current.charAt(this.current.length-1) != " ") {
          this.current += ` ${value} `;
        }
      }
    },
    equals() {
      console.log("before current: " + this.current)
      this.current = !this.current ? "" : this.current;
      console.log("current: " + this.current)
      let result = !this.current
        ? ""
        : eval(this.current.replace(/×/g, "*").replace(/÷/g, "/"));
      this.current =
        result === Infinity || Number.isNaN(result) ? "" : `${result}`;
    },
    backspace() {
      this.current = this.current.slice(0, -1);
    }
  },
  mounted() {
    window.addEventListener("keyup", event => {
      let btns = document.getElementsByClassName("btn");
      btns.forEach(btn => btn.blur());
      if (event.key === "=" || event.key === "Enter") {
        this.equals();
      } else if (event.key === "Escape") {
        this.clear();
      } else if (event.key === "Backspace") {
        this.backspace();
      } else if (event.key === "%") {
        this.percent();
      } else if (event.key === "+") {
        this.append("+");
      } else if (event.key === "-") {
        this.append("-");
      } else if (event.key === "*") {
        this.append("×");
      } else if (event.key === "/") {
        this.append("÷");
      } else if (event.key === ".") {
        this.append(".");
      } else if (48 <= event.keyCode <= 57) {
        for (var i = 48; i <= 57; i++) {
          if (event.keyCode === i) {
            this.append(i - 48);
          }
        }
      }
    });
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator {
  width: 300px;
  height: 400px;
  border-radius: 8px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: minmax(50px, auto);
  background: grey;
  box-shadow: 0 0 55px rgba(0, 0, 0, 0.3);
}
.display {
  grid-column: 1/5;
  grid-row: 1/3;
  border-radius: 5px 5px 0 0;
  font-size: 29px;
  background: rgb(53, 53, 53);
  color: rgb(235, 235, 235);
  display: flex;
  justify-content: center;
  align-items: center;
}
.btn {
  border: 1px solid rgba(0, 0, 0, 0.1);
  font-weight: bold;
  font-size: 18px;
  color: rgba(80, 80, 80, 0.658);
  font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif;
  transition: 150ms;
  cursor: pointer;
}

.btn:focus {
  outline: none;
}
.btn:hover.operator {
  background: rgb(255, 205, 40);
}
.btn:hover:not(.operator) {
  background: rgb(221, 221, 221);
}
.zero {
  grid-column: 1/3;
  border-radius: 0 0 0 5px;
}
.equals {
  border-radius: 0 0 5px 0;
}
.operator {
  background-color: orange;
}
</style>
