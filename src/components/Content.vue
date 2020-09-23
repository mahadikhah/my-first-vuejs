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
      this.Next();
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