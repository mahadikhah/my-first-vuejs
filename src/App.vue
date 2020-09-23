<template>
  <div id="app">
    <Header v-if="questions.length>0" />
    <Content
      v-if="questions.length>0"
      :Question="questions[index]"
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
    hello: function () {
      return "hello";
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
