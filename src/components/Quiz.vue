<template>
  <div v-if="showModal">
    <Modal @close="addQuestion" @showQuestion="showQuestion" />
  </div>
  <h1>Quizly</h1>
  <div class="addQues">
    <button @click="addQuestion">Add Question</button>
  </div>

  <div class="outContainer">
    <div class="container">
      <div class="btn">
        <button v-if="this.b === 1" :disabled="true" @click="prevQuestion">
          Previous
        </button>
        <button v-else :disabled="false" @click="prevQuestion">Previous</button>
        <h3>Question {{ b }}/{{ this.questions.length }}</h3>
        <button
          v-if="this.b <= this.questions.length - 1"
          :disabled="false"
          @click="nextQuestion"
        >
          Next
        </button>
        <button v-else :disabled="true" @click="prevQuestion">Next</button>
      </div>
      <div
        class="quesContainer"
        v-for="(question, index) in questions.slice(a, b)"
        :key="index"
      >
        <p>{{ question.question }}</p>
        <p>A: {{ question.ansA }}</p>
        <p>B: {{ question.ansB }}</p>
        <p>C: {{ question.ansC }}</p>
        <p>D: {{ question.ansD }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import Modal from "./Modal.vue";

export default {
  components: {
    Modal,
  },
  data() {
    return {
      showModal: false,
      questions: [
        {
          question:
            "If the transformation depicted in organelle B requires oxygen, what form of energy is represented by E IV?",
          ansA: "Radiant energy in the form of photons",
          ansB: "Chemical energy being stored as glycogen",
          ansC: "Chemical energy in the form of ATP",
          ansD: "Chemical energy released by glycolysis",
        },
      ],
      a: 0,
      b: 1,
    };
  },
  methods: {
    addQuestion() {
      this.showModal = !this.showModal;
    },
    showQuestion(title, choiceA, choiceB, choiceC, choiceD, answer) {
      console.log(title, choiceA, choiceB, choiceC, choiceD, answer);
      this.questions.push({
        question: title,
        ansA: choiceA,
        ansB: choiceB,
        ansC: choiceC,
        ansD: choiceD,
        answer: answer,
      });
    },
    nextQuestion() {
      this.a++;
      this.b++;
    },
    prevQuestion() {
      this.a--;
      this.b--;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.btn {
  display: flex;
  justify-content: space-between;
  margin-bottom: 25px;
}
.btn h3 {
  margin: 0px;
}
.outContainer {
  display: flex;
  justify-content: center;
}
.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  border-style: solid;
  width: 750px;
  padding: 25px;
  margin: 15px;
}
.quesContainer {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}
</style>
