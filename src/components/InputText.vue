<template>
  <div style="background-color: #ddd">
    Child:
    <!-- childはそのまま入力値を代入する(v-modelの書き換え実装) -->
    <input :value="childMessage" @input="childMessage = $event.target.value" />
    <p>Childの値: {{ childMessage }}</p>
    <p>Childの判定: {{ debug }}</p>
  </div>
</template>

<script>
import { defineComponent } from "@vue/composition-api";

export default defineComponent({
  name: "input-text",
  props: ["message"],
  setup() {},
  data() {
    return {
      // 初期値(本来はあんまり良くないらしい)
      childMessage: this.message,
      debug: "",
    };
  },
  // vue3 から 子->親のemitは事前に宣言しないと Warnが出る
  emits: ["text-box"],
  // computeやmethod(eventハンドリング)ではなく、watchで対応する
  // vueで管理できるイベント発生タイミングにする
  watch: {
    // 親コンポーネントで更新があったとき、子も合わせる
    message(value) {
      this.childMessage = value;
    },
    // 子コンポーネントで更新があったとき、数値以外を除く
    childMessage(value) {
      // 0-9 or '-' or '_' があるかどうか
      const regex = /[^0-9\-_]/;
      const replaced = value.replace(regex, "");
      // まずchildMessageを更新しないようにする
      this.childMessage = replaced;
      // 親コンポーネントに通知する
      this.$emit("text-box", replaced);
    },
  },
});
</script>
