<template>
  <div>
    <div>
      <p>{{ ques.question }}</p>
      <!-- <p v-html="ques.question"></p> -->
      <input
        type="radio"
        id="true"
        :value="ques.incorrect_answers[0]"
        v-model="picked"
        @change="emitCustomEvent"
      />
      <label for="true">{{ ques.incorrect_answers[0] }}</label>
      <input
        type="radio"
        id="true"
        :value="ques.incorrect_answers[1]"
        v-model="picked"
        @change="emitCustomEvent"
      />
      <label for="true">{{ ques.incorrect_answers[1] }}</label>
      <input
        type="radio"
        id="true"
        :value="ques.incorrect_answers[2]"
        v-model="picked"
        @change="emitCustomEvent"
      />
      <label for="true">{{ ques.incorrect_answers[2] }}</label>
      <input
        type="radio"
        id="false"
        :value="ques.correct_answer"
        v-model="picked"
        @change="emitCustomEvent"
      />
      <label for="false">{{ ques.correct_answer }}</label>
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
</style>