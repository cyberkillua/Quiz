<template>
  <div>
    <div>
      <p>{{ ques.question }}</p>
      <!-- <p v-html="ques.question"></p> -->
      <label for="true">
        <input
          type="radio"
          id="true"
          :value="ques.incorrect_answers[0]"
          v-model="picked"
          @change="emitCustomEvent"
        />
        {{ ques.incorrect_answers[0] }}</label
      >
      <label for="true"
        ><input
          type="radio"
          id="true"
          :value="ques.incorrect_answers[1]"
          v-model="picked"
          @change="emitCustomEvent"
        />
        {{ ques.incorrect_answers[1] }}</label
      >
      <label for="true"
        ><input
          type="radio"
          id="true"
          :value="ques.incorrect_answers[2]"
          v-model="picked"
          @change="emitCustomEvent"
        />
        {{ ques.incorrect_answers[2] }}</label
      >
      <label for="false"
        ><input
          type="radio"
          id="false"
          :value="ques.correct_answer"
          v-model="picked"
          @change="emitCustomEvent"
        />
        {{ ques.correct_answer }}</label
      >
    </div>
  </div>
</template>

<script>
export default {
  name: "Displayq",
  components: {},
  data() {
    return {
      picked: null,
    };
  },

  props: ["ques"],
  methods: {
    emitCustomEvent() {
      if (this.picked === this.ques.correct_answer) {
        console.log("correct");
        this.$emit("answer", 10);
      }
    },
  },
};
</script>

<style scoped>
label {
  display: block;
}
</style>