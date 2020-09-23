<template>
  <div class="content">
    <b-container class="bv-example-row">
      <b-row align-v="center">
        <b-col md="2"></b-col>
        <b-col md="8">
          <b-card no-body header-tag="header">
            <!------------------------- -card header  here ------------------------>
            <template v-slot:header>
              <b>
                <span>{{index+1}})</span>
                <!-- question is here --------------------------- -->
                {{Question.question}}
              </b>
            </template>
            <!-- card body ------------------------ -->
            <b-card-body>
              <div class="T-center" style="margin-top:25px; min-height:200px">
                <b-list-group>
                  <!-- questino answers here ----------------------- -->
                  <b-list-group-item
                    href="#"
                    v-for="(choice,index) in Question.answers"
                    :key="index"
                    @click="selected(index)"
                  >{{choice}}</b-list-group-item>
                </b-list-group>
              </div>
            </b-card-body>
            <b-card-footer>
              <b-row align-v="end">
                <b-col cols="1"></b-col>
                <b-col cols="2">
                  <b-button v-if="index!==0" variant="outline-danger" @click="back">back</b-button>
                </b-col>
                <b-col md="6" align-self="center"></b-col>
                <b-col cols="3">
                  <b-button v-if="index===9" variant="outline-primary" @click="back">submit</b-button>
                  <b-button
                    v-if="index!==9"
                    variant="outline-success"
                    @click="next"
                    :disabled="!choosed"
                  >next</b-button>
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
      choosed: false,
      // q: this.props.Question,
    };
  },
  //--------------------------------------------------------------------------------
  methods: {
    selected: function (index) {
      console.log(
        `this.answers.length${this.answers.length}`,
        `this.index${this.index}`,
        `this.answers${this.answers}`
      );
      this.choosed = true;
      this.answers[this.index] = index;
      // this.Next();
    },
    next: function () {
      this.Next();
      console.log(
        `this.answers.length${this.answers.length}`,
        `this.index${this.index}`,
        `this.answers${this.answers}`
      );
      if (this.index >= this.answers.length - 1) {
        this.choosed = false;
        console.log("index>=this.answers.length-1");
      }
    },
    back: function () {
      this.Back();
      console.log(
        `this.answers.length${this.answers.length}`,
        `this.index${this.index}`,
        `this.answers${this.answers}`
      );
      if (this.index <= this.answers.length) {
        this.choosed = true;
        console.log("index<this.answers.length");
      }
    },
  },

  //--------------------------------------------------------------------------------

  computed: {
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