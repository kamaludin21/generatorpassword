<template>
  <div id="app" class="flex flex-col h-screen bg-gray-200">
    <div class="flex-grow">
      <div
        class="relative w-full sm:w-3/5 md:w-1/2 lg:w-1/3 mx-auto p-2 space-y-2"
      >
        <Title />
        <PasswordResult
          :randomPassword="randomPassword"
          @copy-password="copyClipPassword($event)"
        />
        <input type="hidden" id="clipboard" :value="randomPassword" />
        <transition name="slide-fade">
          <div
            class="absolute right-0 top-4 mr-2 bg-green-200 rounded-md"
            v-show="copied"
          >
            <p class="text-lg font-medium p-2 tracking-wide">Disalin!</p>
          </div>
        </transition>
        <Setting />
      </div>
    </div>
    <Footer />
  </div>
</template>

<script>
import Title from "./components/Title";
import PasswordResult from "./components/PasswordResult";
import Setting from "./components/Setting";
import Footer from "./components/Footer";

export default {
  name: "App",
  components: {
    Title,
    PasswordResult,
    Setting,
    Footer,
  },
  data() {
    return {
      randomPassword: "",
      length: 16,
      characterType:
        "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789!@#$%^&*()_+=",
      copied: false,
    };
  },
  methods: {
    generatePassword: function (characterLength, characterType) {
      let i;
      let password = "";
      for (i = 0; i < characterLength; i++) {
        password += characterType.charAt(
          Math.floor(Math.random() * characterType.length)
        );
      }
      return (this.randomPassword = password);
    },
    copyClipPassword: function() {
      this.copied = true;
      let copyText = document.querySelector("#clipboard");
      copyText.setAttribute("type", "text");
      copyText.select();
      try {
        document.execCommand("copy");
        setTimeout(() => {
          this.copied = false;
        }, 1000);
      } catch (err) {
        alert("Oops, unable to copy");
      }
      copyText.setAttribute("type", "hidden");
      window.getSelection().removeAllRanges();
    },
  },
  beforeMount() {
    this.generatePassword(this.length, this.characterType);
  },
};
</script>

<style>
.slide-fade-leave-active {
  transition: all 0.8s cubic-bezier(1, 0.5, 0.8, 1);
}
.slide-fade-enter, .slide-fade-leave-to
/* .slide-fade-leave-active below version 2.1.8 */ {
  transform: translateX(5px);
  opacity: 0;
}
</style>
