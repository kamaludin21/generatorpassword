<template>
  <div
    class="
      bg-white
      flex
      items-center
      px-2
      py-3
      shadow-lg
      rounded
      border-t-4 border-green-600
    "
  >
    <div class="flex-1 overflow-auto">
      <p class="text-2xl font-semibold text-center">
        {{ randomPassword }}
      </p>
    </div>
    <div
      class="flex-shrink-0 hover:bg-green-200 rounded p-1 cursor-pointer"
      @click="copyPassword()"
    >
      <svg
        xmlns="http://www.w3.org/2000/svg"
        class="h-7 w-7"
        fill="none"
        viewBox="0 0 24 24"
        stroke="currentColor"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="2"
          d="M8 16H6a2 2 0 01-2-2V6a2 2 0 012-2h8a2 2 0 012 2v2m-6 12h8a2 2 0 002-2v-8a2 2 0 00-2-2h-8a2 2 0 00-2 2v8a2 2 0 002 2z"
        />
      </svg>
    </div>
  </div>
</template>

<script>
export default {
  name: "PasswordResult",
  props: {
    randomPassword: String,
  },
  methods: {
    copyPassword: function () {
      this.$emit("copy-password", this.randomPassword);
    },
  },
};
</script>
