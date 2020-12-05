<template>
  <div id="app">
    <div class="question-div">
      <h2 v-if="displayScore">Your final is {{ score }} points</h2>
      <div v-bind:key="ques.id" v-for="ques in questions">
        <Displayq :ques="ques" @answer="calScore" />
      </div>
      <button @click="showScore">Sumbit</button>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Displayq from "./components/Displayq.vue";
import he from "he";
export default {
  name: "App",
  data() {
    return {
      questions: [],
      score: 0,
      displayScore: false,
    };
  },
  components: {
    Displayq,
  },
  methods: {
    calScore(mark) {
      this.score = this.score + mark;
      // {this.answersPicked = this.answersPicked.push(data)}
      // console.log(this.answersPicked);
    },
    showScore() {
      this.displayScore = true;
    },
  },

  created() {
    axios
      .get(
        "https://opentdb.com/api.php?amount=5&category=9&difficulty=easy&type=multiple"
      )
      .then((res) => {
        this.questions = res.data.results.map((questionObject) => ({
          ...questionObject,
          question: he.decode(questionObject.question),
          correct_answer: he.decode(questionObject.correct_answer),
          incorrect_answers: questionObject.incorrect_answers.map((ans) => {
            return he.decode(ans);
          }),
        }));
      })
      .catch((err) => console.log(err));
  },
};
</script>

<style>
#app {
  margin: 0;
  padding: 0;
}
.question-div{
  /* background-color: yellow; */
  padding: 25px;
   line-height: 1.6;
}
button {
  font-family: "Roboto", sans-serif;
  text-transform: uppercase;
  outline: 0;
  background: #065784;
  width: 100px;
  border: 0;
  justify-self: center;
  align-self: center;
  padding: 15px;
  color: #ffffff;
  font-size: 14px;
  -webkit-transition: all 0.3 ease;
  transition: all 0.3 ease;
  cursor: pointer;
}
</style>
