<template>
  Child: <input :value="childMessage" @input="handle($event)" />
  <p>Childの値: {{ childMessage }}</p>
  <p>Childの判定: {{ debug }}</p>
</template>

<script>
import { getCurrentInstance, defineComponent } from "@vue/composition-api";

export default defineComponent({
  name: "input-text",
  props: ["message"],
  setup() {},
  data() {
    return {
      debug: "",
    };
  },
  computed: {
    childMessage() {
      return this.message;
    },
  },
  methods: {
    handle(e) {
      const message = e.target.value;
      const regex = /[^0-9]/g;
      this.debug =
        regex.test(message) +
        ": " +
        e.target.value +
        ": ->" +
        message.replace(regex, "");

      this.childMessage = message.replace(regex, "");

      this.$emit("text-box", message.replace(regex, ""));
      const instance = getCurrentInstance();
      instance?.proxy?.$forceUpdate();
    },
  },
});
</script>
