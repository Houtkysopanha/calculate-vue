<template>
  <div class="main-content">
    <div class="main">
      <div
        class="Calculator"
        style="box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3); padding: 12px; border-radius: 15px;"
      >
        <div class="form">
          <div class="header">
            <h6 style="color: whitesmoke;">Calculate</h6>
            <hr style="color: aliceblue;" />
          </div>
          <div class="display-text mb-4">
            <input
              style="width: 100%; height: 120px;"
              type="text"
              v-model="input"
              readonly
            />
          </div>
          <br />
          <div class="button text-center">
            <div class="row row-cols-0 row-cols-md-4 g-2 g-md-3">
              <!-- Number Buttons -->
              <div class="col" v-for="btn in numberButtons" :key="btn">
                <div class="p-0 mb-4">
                  <button @click="appendNumber(btn)" class="btn btn--secondary">
                    {{ btn }}
                  </button>
                </div>
              </div>

              <!-- Operator Buttons -->
              <div class="col" v-for="operator in operatorButtons" :key="operator">
                <div class="p-0 mb-4">
                  <button
                    @click="appendOperator(operator)"
                    class="btn btn--secondary"
                  >
                    {{ operator }}
                  </button>
                </div>
              </div>
            </div>

            <!-- Clear and Equals -->
            <div class="row row-cols-0 row-cols-md-2 g-2 g-md-3">
              <div class="col">
                <div class="p-1 mt-2">
                  <button
                    style="width: 100%;"
                    @click="clearInput"
                    class="btn btn--secondary"
                  >
                    C
                  </button>
                </div>
              </div>
              <div class="col">
                <div class="p-1 mt-2">
                  <button
                    style="width: 100%;"
                    @click="calculateResult"
                    class="btn btn--secondary"
                  >
                    =
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "CalForm",
  data() {
    return {
      input: "",
      numberButtons: [7, 8, 9, 4, 5, 6, 1, 2, 3, 0, "."],
      operatorButtons: ["DEL", "+", "-", "/", "x"],
    };
  },
  methods: {
    appendNumber(number) {
      this.input += number.toString();
    },
    appendOperator(operator) {
      if (operator === "DEL") {
        this.input = this.input.slice(0, -1);
      } else {
        this.input += operator === "x" ? "*" : operator;
      }
    },
    clearInput() {
      this.input = "";
    },
    calculateResult() {
      try {
        this.input = eval(this.input).toString();
      } catch {
        this.input = "Error";
      }
    },
  },
};
</script>

<style scoped>
.main-content {
  width: 100%;
  height: auto;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 8rem;
}

.Calculator {
  width: 100%;
  max-width: 500px;
  padding: 12px;
  border-radius: 15px;
}

.display-text input {
  border-radius: 15px;
  border: none;
  background-color: #374151;
  font-size: 3rem;
  font-weight: 500;
  text-align: end;
  color: whitesmoke;
  height: 120px;
}

.btn {
  position: relative;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 6px;
  background-color: var(--btn-bg);
  padding: 5px 40px;
  width: 100px;
  height: 50px;
  border-radius: 8px;
  border: 0;
  cursor: pointer;
  font-weight: 600;
  font-size: 2rem;
  font-family: system-ui;
  border: 2px solid var(--btn-color);
  transition: 100ms ease;
  box-shadow: 0px 5px 0 0 var(--btn-color);
}

.btn--secondary {
  --btn-color: black;
  --btn-bg: #fafafa;
}

.btn svg {
  width: 20px;
  height: 20px;
  flex-shrink: 0;
}

.btn:hover {
  box-shadow: 0px 5px 0 0 var(--btn-color);
}

.btn:active {
  transition: 50ms ease;
  box-shadow: 0 0 0 0 var(--btn-color);
}

.btn:focus-visible {
  outline: 0;
}

@media (max-width: 768px) {
  .display-text input {
    font-size: 2rem; /* Smaller font size for tablets */
    height: 100px; /* Adjust height */
  }

  .btn {
    height: 45px;
    font-size: 1rem; /* Adjust font size */
  }

  .row-cols-md-4 {
    flex-basis: 23%; /* 4 buttons per row on larger screens */
  }
}

@media (max-width: 576px) {
  .Calculator {
    width: 100%;
    max-width: 400px; /* Restrict the width of the calculator */
  }

  .display-text input {
    font-size: 1.5rem;
    height: 80px;
  }

  .btn {
    flex: 1 0 calc(33.33% - 1rem); /* 3 buttons per row */
    max-width: calc(33.33% - 1rem);
    height: 40px;
    font-size: 1rem;
  }

  .row-cols-md-4 {
    flex-basis: 33%; /* Make buttons fit better */
  }
}
</style>
