<template>
  <div>
  <div
    class="w-full bg-white p-4 shadow-lg rounded border-t-4 border-green-600"
  >
    <p class="text-lg font-medium mb-2 select-none">Jumlah karakter</p>
    <div class="flex w-full items-center space-x-4">
      <div class="flex-shrink-0 text-lg text-center">
        <input
          type="text"
          v-model="length"
          size="1"
          class="border-2 text-center border-gray-400 rounded bg-gray-200"
        />
      </div>
      <div class="flex-1">
        <input
          type="range"
          class="w-full select-none"
          min="6"
          max="30"
          step="1"
          v-model="length"
        />
      </div>
    </div>
    <p class="text-lg font-medium mb-2 select-none">Paramater lain</p>
    <div class="flex flex-col space-y-2">
      <label class="container"
        >Uppercase
        <!-- Check jika array.length == 1, jika isinya sama, aktifkan disabled -->
        <input
          type="checkbox"
          v-model="parameter"
          value="uppercase"
          checked
          :disabled="
            parameter.length == 1 && parameter.includes('uppercase')
              ? true
              : false
          "
        />
        <span class="checkmark"></span>
      </label>
      <label class="container"
        >Lowercase
        <input
          type="checkbox"
          v-model="parameter"
          value="lowercase"
          checked
          :disabled="
            parameter.length == 1 && parameter.includes('lowercase')
              ? true
              : false
          "
        />
        <span class="checkmark"></span>
      </label>
      <label class="container"
        >Number
        <input
          type="checkbox"
          v-model="parameter"
          value="number"
          checked
          :disabled="
            parameter.length == 1 && parameter.includes('number') ? true : false
          "
        />
        <span class="checkmark"></span>
      </label>
      <label class="container"
        >Symbol
        <input
          type="checkbox"
          v-model="parameter"
          value="symbol"
          checked
          :disabled="
            parameter.length == 1 && parameter.includes('symbol') ? true : false
          "
        />
        <span class="checkmark"></span>
      </label>
    </div>
  </div>
  <div class="flex space-x-2 my-2">
    <button
      class="
        flex-1
        py-4
        bg-green-600
        rounded
        border-green-400
        hover:bg-green-500 hover:text-white
        font-bold
        text-gray-200
        hover:text-gray-800
        select-none
      "
      @click="generatePasswordOnClick()"
    >
      GENERATE
    </button>
  </div>
  </div>
</template>

<script>
export default {
  name: "Setting",
  data() {
    return {
      length: 16,
      parameter: ["uppercase", "lowercase", "number", "symbol"],
    };
  },
  watch: {
    length() {
      let characterType = this.procesParameter(this.parameter);
      this.$parent.generatePassword(this.length, characterType);
    },
    parameter() {
      let characterType = this.procesParameter(this.parameter);
      this.$parent.generatePassword(this.length, characterType);
    },
  },
  methods: {
    procesParameter: function (value) {
      let uppercase = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
      let lowercase = "abcdefghijklmnopqrstuvwxyz";
      let number = "0123456789";
      let symbol = "!@#$%^&*()_+=";

      let char = "";
      value.includes("uppercase") ? (char += uppercase) : "";
      value.includes("lowercase") ? (char += lowercase) : "";
      value.includes("number") ? (char += number) : "";
      value.includes("symbol") ? (char += symbol) : "";
      return char;
    },
    generatePasswordOnClick: function () {
      let characterType = this.procesParameter(this.parameter);
      this.$parent.generatePassword(this.length, characterType);
    },
  },
};
</script>

<style scoped>
/* slider */
input[type="range"] {
  height: 32px;
  -webkit-appearance: none;
  margin: 10px 0;
  width: 100%;
}
input[type="range"]:focus {
  outline: none;
}
input[type="range"]::-webkit-slider-runnable-track {
  width: 100%;
  height: 5px;
  cursor: pointer;
  animate: 0.2s;
  box-shadow: 0px 0px 0px #000000;
  background: #059669;
  border-radius: 49px;
  border: 0px solid #000000;
}
input[type="range"]::-webkit-slider-thumb {
  box-shadow: 0px 0px 0px #000000;
  border: 2px solid #047857;
  height: 25px;
  width: 25px;
  border-radius: 25px;
  background: #059669;
  cursor: pointer;
  -webkit-appearance: none;
  margin-top: -10.5px;
}
input[type="range"]:focus::-webkit-slider-runnable-track {
  background: #059669;
}
input[type="range"]::-moz-range-track {
  width: 100%;
  height: 5px;
  cursor: pointer;
  animate: 0.2s;
  box-shadow: 0px 0px 0px #000000;
  border-radius: 49px;
  border: 0px solid #000000;
}
input[type="range"]::-moz-range-thumb {
  box-shadow: 0px 0px 0px #000000;
  border: 1px solid #059669;
  height: 25px;
  width: 25px;
  border-radius: 25px;
  background: #059669;
  cursor: pointer;
}
input[type="range"]::-ms-track {
  width: 100%;
  height: 5px;
  cursor: pointer;
  animate: 0.2s;
  background: transparent;
  border-color: transparent;
  color: transparent;
}
input[type="range"]::-ms-fill-lower {
  background: #43e33d;
  border: 0px solid #000000;
  border-radius: 98px;
  box-shadow: 0px 0px 0px #000000;
}
input[type="range"]::-ms-fill-upper {
  background: #43e33d;
  border: 0px solid #000000;
  border-radius: 98px;
  box-shadow: 0px 0px 0px #000000;
}
input[type="range"]::-ms-thumb {
  margin-top: 1px;
  box-shadow: 0px 0px 0px #000000;
  border: 1px solid #059669;
  height: 25px;
  width: 25px;
  border-radius: 25px;
  background: #059669;
  cursor: pointer;
}
input[type="range"]:focus::-ms-fill-lower {
  background: #059669;
}
input[type="range"]:focus::-ms-fill-upper {
  background: #059669;
}

/* Checkbox */
/* Hide the browser's default checkbox */
.container {
  display: block;
  position: relative;
  padding-left: 35px;
  /* background: #ccc; */
  cursor: pointer;
  font-size: 18px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

/* Hide the browser's default checkbox */
.container input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}

/* Create a custom checkbox */
.checkmark {
  position: absolute;
  top: 0px;
  left: 0;
  height: 25px;
  width: 25px;
  border: 2px solid #047857;
  border-radius: 4px;
  background-color: #eee;
}

/* On mouse-over, add a grey background color */
.container:hover input ~ .checkmark {
  background-color: #ccc;
}

/* When the checkbox is checked, add a blue background */
.container input:checked ~ .checkmark {
  background-color: #059669;
}

/* Create the checkmark/indicator (hidden when not checked) */
.checkmark:after {
  content: "";
  position: absolute;
  display: none;
}

/* Show the checkmark when checked */
.container input:checked ~ .checkmark:after {
  display: block;
}

/* Style the checkmark/indicator */
.container .checkmark:after {
  left: 8px;
  top: 5px;
  width: 5px;
  height: 10px;
  border: solid white;
  border-width: 0 3px 3px 0;
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  transform: rotate(45deg);
}
</style>
