<template>
  <div class="question-box-container">
    <b-jumbotron>
      <template v-slot:lead>
        {{ currentQuestion.question }}
      </template>

      <hr class="my-4" />

      <b-list-group class="mb-3">
        <b-list-group-item 
          v-for="(ans, index) in answers"
          :key="index"
          @click.prevent="selectAnswer(index)"
          :class="[selectedItem === index ? 'selected' : '']"
          >{{ ans }}          
        </b-list-group-item>
      </b-list-group>

      <b-button variant="primary" href="#">Submit</b-button>
      <b-button variant="success" href="#" @click="next" class="ml-3">
        Next
      </b-button>
    </b-jumbotron>
  </div>
</template>

<script>
export default {
  name: "QuestionBox",
  props: {
    currentQuestion: Object,
    next: Function,
  },
  data(){
    return {
      selectedItem: null
    }
  },
  methods:{
    selectAnswer(index){
      this.selectedItem = index
    }
  },
  computed:{
    answers(){
      let answers = [...this.currentQuestion.incorrect_answers]
      answers.push(this.currentQuestion.correct_answer)
      return answers
    }
  },
  mounted() {},
};
</script>

<style scoped>
  .list-group-item:hover {
    background-color: lightblue;
    cursor: pointer;
  }
  .selected {
    background-color: indianred !important;
    color: white;
  }
</style>