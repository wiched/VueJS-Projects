<template>
  <div class="component">
    <h3>You may view the User Details here</h3>
    <p>Many Details</p>
    <p>User Name: {{switchName()}}</p>
    <p>User age: {{userAge}}</p>
    <button @click="resetName">Reset the name</button>
    <button @click="resetFn()">Reset the name</button>
  </div>
</template>

<script>
import { eventBus } from "../main.js";
export default {
  props: {
    name: {
      type: String,
      required: true
    },
    resetFn: {
      type: Function
    },
    userAge: Number
  },
  methods: {
    switchName() {
      return this.name
        .split("")
        .reverse()
        .join("");
    },
    resetName() {
      this.name = "Lubo";
      this.$emit("nameWasReset", this.name);
    }
  },
  created() {
    eventBus.$on("ageWasEdited", data => {
      this.userAge = data;
    });
  }
};
</script>

<style scoped>
div {
  background-color: lightcoral;
}
</style>
