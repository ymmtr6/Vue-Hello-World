<template>
  <div class="hello">
    <input-text @text-box="updateEvent" :message="message" />
    <p>Parentの値: {{ message }}</p>
    Parent: <input v-model="message" />
  </div>
</template>

<script>
import InputText from "./InputText.vue";
export default {
  components: { InputText },
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      message: "000",
    };
  },
  methods: {
    updateEvent(msg) {
      this.message = msg;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
