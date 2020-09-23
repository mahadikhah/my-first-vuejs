<template>
  <div class="content">
    <b-container class="bv-example-row">
      <b-row align-v="center">
        <b-col md="2"></b-col>
        <b-col md="8">
          <b-card no-body header-tag="header">
            <!-- <b-card-text>here list should update</b-card-text> -->
            <template v-slot:header>
              <b>
                <span>{{index+1}})</span>
                {{Question.question}}
              </b>
            </template>
            <b-card-body>
              <div class="T-center" style="margin-top:25px; min-height:200px">
                <b-list-group>
                  <b-list-group-item
                    href="#"
                    v-for="(choice,index) in choices"
                    :key="index"
                    @click="selected(index)"
                  >{{choice}}</b-list-group-item>
                </b-list-group>
              </div>
            </b-card-body>
            <b-card-footer>
              <b-row align-v="end">
                <b-col cols="3">
                  <b-button v-if="index!==0" variant="outline-primary" @click="Back">back</b-button>
                </b-col>
                <b-col cols="6"></b-col>
                <b-col cols="3">
                  <b-button v-if="index!==9" variant="outline-primary" @click="Next">next</b-button>
                </b-col>
              </b-row>
            </b-card-footer>
          </b-card>
        </b-col>
        <b-col md="2"></b-col>
      </b-row>
    </b-container>
  </div>
</template>
<script>
export default {
  name: "Content",
  //--------------------------------------------------------------------------------

  props: {
    Question: Object,
    Next: Function,
    Back: Function,
    index: Number,
  },
  //--------------------------------------------------------------------------------

  data() {
    return {
      answers: [],
      answerSheet: [],
      // q: this.props.Question,
    };
  },
  //--------------------------------------------------------------------------------
  methods: {
    selected: function (index) {
      this.answers[this.index] = index;
      // console.log(this.answers, this.answerSheet);
      this.Next();
    },
    makeAnswerSheet: function (correct) {
      this.answerSheet[this.index] = correct;
      console.log(this.answerSheet);
    },
  },

  //--------------------------------------------------------------------------------

  computed: {
    choices: function () {
      const incorrect_answers = [...this.Question.incorrect_answers];
      const correct_answer = this.Question.correct_answer;
      let all = incorrect_answers.concat(correct_answer);
      let correct = all.length - 1;
      for (let i = all.length - 1; i > 0; i--) {
        let j = Math.floor(Math.random() * i);
        // if (correct === i)
        if (j == correct) {
          correct = i;
        } else if (i == correct) {
          correct = j;
        }

        let k = all[i];
        all[i] = all[j];
        all[j] = k;
      }
      this.makeAnswerSheet(correct);
      // this.answerSheet[this.index] = correct;
      // console.log(correct, all, correct_answer, incorrect_answers, this.index);
      return all;
    },
    //-----------------
  },
};
</script>



<style scoped>
.T-center {
  text-align: center;
}
.content {
  height: 100vh;
  margin-top: 50px;
}
</style>