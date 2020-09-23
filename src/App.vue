<template>
  <div id="app">
    <Header v-if="questions.length>0" />
    <Content
      v-if="questions.length>0"
      :Question="randomAnswerSortedQuestions[index]"
      :Next="next"
      :Back="back"
      :index="index"
    />
    <!--  loading spinner  -->
    <!-- {{hello}} -->
    <div v-if="spinner" class="d-flex align-items-center spinner">
      <b-spinner variant="primary" label="Text Centered" type="grow"></b-spinner>loading
    </div>
  </div>
</template> 
<script>
import Content from "./components/Content";
import Header from "./components/Header";
import axios from "axios";

export default {
  name: "App",
  //--------------------------------------------------------------------------------
  data() {
    return {
      questions: [],
      spinner: true,
      index: 0,
    };
  },

  //--------------------------------------------------------------------------------

  components: {
    Header,
    Content,
  },
  //--------------------------------------------------------------------------------
  methods: {
    next: function () {
      this.index =
        this.index < this.questions.length - 1 ? this.index + 1 : this.index;
      // console.log(this.questions.length, this.index);
    },
    back: function () {
      this.index = this.index > 0 ? this.index - 1 : this.index;
    },
  },
  //--------------------------------------------------------------------------------
  computed: {
    randomAnswerSortedQuestions: function () {
      let question = this.questions;
      let sorted = [];
      question.forEach((element, key) => {
        element.answers = element.incorrect_answers.concat(
          element.correct_answer
        );
        let correct = element.answers.length - 1;
        for (let i = element.answers.length - 1; i > 0; i--) {
          let j = Math.floor(Math.random() * i);
          if (j == correct) {
            correct = i;
          } else if (i == correct) {
            correct = j;
          }
          let k = element.answers[i];
          element.answers[i] = element.answers[j];
          element.answers[j] = k;
        }
        element.correct_answer_key = correct;
        sorted[key] = {
          question: element.question,
          answers: element.answers,
          correct_answer_key: element.correct_answer_key,
        };
      });
      // console.log(question);
      return sorted;
    },
  },

  //--------------------------------------------------------------------------------

  mounted: function () {
    axios
      .get("https://opentdb.com/api.php?amount=10&category=21")
      .then((res) => {
        // console.log(res.data.results);
        this.questions = res.data.results;
        this.spinner = false;
      });
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
}
/*  --------------------- */
.spinner {
  position: absolute;
  left: 50%;
  top: 50%;
}
</style>
