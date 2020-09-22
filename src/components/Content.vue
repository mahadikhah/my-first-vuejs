<template>
  <div class="content">
    <b-container class="bv-example-row">
      <b-row align-v="center">
        <b-col md="2"></b-col>
        <b-col md="8">
          <b-card header-tag="header">
            <!-- <b-card-text>here list should update</b-card-text> -->
            <template v-slot:header>
              <b>
                <span>{{index+1}})</span>
                {{Question.question}}
              </b>
            </template>

            <div class="T-center" style="margin-top:25px; min-height:150px">
              <div v-for="(choice,index) in choices" :key="index">
                <b-card-text>{{choice}}</b-card-text>
              </div>
              <!-- <b-card-text>A second paragraph of text in the card.</b-card-text>
              <b-card-text>A second paragraph of text in the card.</b-card-text>
              <b-card-text>A second paragraph of text in the card.</b-card-text>-->
              <b-row>
                <b-col cols="3">
                  <b-button v-if="index!==0" variant="outline-primary" @click="Back">back</b-button>
                </b-col>
                <b-col cols="6"></b-col>
                <b-col cols="3">
                  <b-button v-if="index!==9" variant="outline-primary" @click="Next">next</b-button>
                </b-col>
              </b-row>
            </div>
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
      // q: this.props.Question,
    };
  },
  //--------------------------------------------------------------------------------
  methods: {
    random: function () {
      // console.log(all);
      // console.log(answers.splice(random, 4, correct_answer));
    },
  },

  //--------------------------------------------------------------------------------

  computed: {
    choices: function () {
      const incorrect_answers = [...this.Question.incorrect_answers];
      const correct_answer = this.Question.correct_answer;
      let all = incorrect_answers.concat(correct_answer);
      for (let i = all.length - 1; i > 0; i--) {
        let j = Math.floor(Math.random() * i);
        let k = all[i];
        all[i] = all[j];
        all[j] = k;
      }
      return all;
    },
  },
};
</script>



<style >
.T-center {
  text-align: center;
}
.content {
  height: 100vh;
  margin-top: 50px;
}
</style>