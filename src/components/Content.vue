<template>
  <div class="content">
    <b-container class="bv-example-row">
      <b-row align-v="center">
        <b-col md="2"></b-col>
        <b-col md="8">
          <b-card v-if="!submited" no-body header-tag="header">
            <!------------------------- -card header  here ------------------------>
            <template v-slot:header>
              <b>
                <span>{{ index + 1 }})</span>
                <!-- question is here --------------------------- -->
                <span v-once>
                  {{ Question.question }}
                </span>
              </b>
            </template>
            <!-- card body ------------------------ -->
            <b-card-body>
              <b-alert
                v-if="
                  answers[index] === Question.correct_answer_key && resultsMode
                "
                show
                variant="success"
                >you choosed the TRUE answer</b-alert
              >
              <b-alert
                v-if="
                  answers[index] !== Question.correct_answer_key && resultsMode
                "
                show
                variant="danger"
                >you choosed the WRONG answer</b-alert
              >
              <div class="T-center" style="margin-top: 5px; min-height: 200px">
                <!-- questino answers here ----------------------- -->
                <!-- questino answers here ----------------------- -->
                <!-- questino answers here ----------------------- -->
                <!-- questino answers here ----------------------- -->
                <b-list-group>
                  <b-list-group-item
                    href="#"
                    v-for="(choice, i) in Question.answers"
                    :key="i"
                    @click="selected(i)"
                    :class="[
                      i == answers[index] && !resultsMode
                        ? 'choosed'
                        : i === Question.correct_answer_key && resultsMode
                        ? 'trueAns'
                        : i === answers[index] &&
                          answers[index] !== Question.correct_answer_key &&
                          resultsMode
                        ? 'falseAns'
                        : '',
                    ]"
                  >
                    <span></span>

                    <span>{{ choice }}</span>
                  </b-list-group-item>
                </b-list-group>

                <!-- questino answers here ----------------------- -->
                <!-- questino answers here ----------------------- -->
                <!-- questino answers here ----------------------- -->
                <!-- questino answers here ----------------------- -->
                <!-- questino answers here ----------------------- -->
              </div>
            </b-card-body>
            <b-card-footer>
              <b-row align-v="end">
                <b-col cols="1"></b-col>
                <b-col cols="2">
                  <b-button
                    v-if="index !== 0"
                    variant="outline-danger"
                    @click="back"
                    >back</b-button
                  >
                </b-col>
                <b-col md="6" align-self="center"></b-col>
                <b-col cols="3">
                  <b-button
                    v-if="index === 9 && !resultsMode"
                    variant="outline-primary"
                    @click="submit"
                    :disabled="!choosed"
                    >submit</b-button
                  >
                  <b-button
                    v-if="index !== 9"
                    variant="outline-success"
                    @click="next"
                    :disabled="!choosed"
                    >next</b-button
                  >
                </b-col>
              </b-row>
            </b-card-footer>
          </b-card>
          <b-card v-if="submited">
            <b-card-body>
              your score is : {{ finalScore }}/10
              <b-button variant="success" @click="showResults"
                >view more results</b-button
              >
            </b-card-body>
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
    resetIndex: Function,
    finalScore: Number,
    result: Function,
  },
  //--------------------------------------------------------------------------------

  data() {
    return {
      answers: [],
      submited: false,
      resultsMode: false,
      choosed: false,
    };
  },
  //--------------------------------------------------------------------------------
  methods: {
    submit: function () {
      this.submited = true;
      this.result(this.answers);
    },
    showResults: function () {
      this.resetIndex();
      this.resultsMode = true;
      this.submited = false;
    },
    selected: function (i) {
      if (!this.resultsMode) {
        this.choosed = true;
        let save = [...this.answers];
        save[this.index] = i;
        this.answers = [...save];
      }
    },
    next: function () {
      this.Next();
      if (this.index >= this.answers.length - 1) {
        this.choosed = false;
      }
    },
    back: function () {
      this.Back();

      if (this.index <= this.answers.length) {
        this.choosed = true;
      }
    },
  },

  //--------------------------------------------------------------------------------
  watch: {},
  //--------------------------------------------------------------------------------

  computed: {},
};
</script>



<style scoped>
.content {
  transform: translate(3, 3);
  transition: 2s all;
}
.T-center {
  text-align: center;
}
.content {
  height: 100vh;
  margin-top: 50px;
}
.choosed {
  background-color: lightblue !important;
}
.trueAns {
  background-color: lightgreen !important;
}
.falseAns {
  background-color: lightcoral !important;
}
</style>