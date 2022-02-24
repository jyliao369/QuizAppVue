<template>
  <div v-if="showModal">
    <Modal @close="addQuestion" @showQuestion="showQuestion" />
  </div>
  <div class="title"><h1>Quizly</h1></div>

  <div class="addQues">
    <!-- <button @click="addQuiz">Add New Quiz</button> -->
    <button @click="addQuestion">Add Question</button>
    <button @click="testScore">test</button>
  </div>

  <div class="overCont">
    <div class="container">
      <!-- THIS IS THE SCOPRE SECTION -->
      <div class="infoHead">
        <div>
          <h2>Question {{ b }}/{{ this.questions.length }}</h2>
        </div>
        <div>
          <h2>Score: {{ score }}</h2>
        </div>
      </div>
      <!-- THIS IS THE QUESTION AND ANSWER SECTION -->
      <div class="quesContainer">
        <div
          class="question"
          v-for="(question, index) in questions.slice(a, b)"
          :key="index"
        >
          <div class="quesTitle">
            <p>{{ question.question }}</p>
          </div>
          <div class="choiceCont">
            <div class="choice">
              <p @click="checkCorrect('A')">A: {{ question.ansA }}</p>
            </div>
            <div class="choice">
              <p @click="checkCorrect('B')">B: {{ question.ansB }}</p>
            </div>
            <div class="choice">
              <p @click="checkCorrect('C')">C: {{ question.ansC }}</p>
            </div>
            <div class="choice">
              <p @click="checkCorrect('D')">D: {{ question.ansD }}</p>
            </div>
          </div>
        </div>
      </div>
      <!-- THIS IS THE BUTTON SECTION -->
      <div class="btnContainer">
        <div class="btnBackground">
          <button v-if="this.b === 1" :disabled="true" @click="prevQuestion">
            Previous
          </button>
          <button v-else :disabled="false" @click="prevQuestion">
            Previous
          </button>
        </div>
        <div class="btnBackground">
          <button
            v-if="this.b <= this.questions.length - 1"
            :disabled="false"
            @click="nextQuestion"
          >
            Next
          </button>
          <button v-else :disabled="true" @click="prevQuestion">Next</button>
        </div>
      </div>
    </div>
  </div>

  <!-- <div class="outContainer">
    <div class="container">
      
    </div>
  </div> -->
  <!-- <div
    class="quizContainer"
    v-for="(quiz, index) in testArray"
    :key="index"
    v-cloak
  >
    {{ testArray[index] }}
    {{ testArray[index].length }}
  </div> -->
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
      testArray: [
        {
          Chemistry: [],
        },
        {
          Biology: [],
        },
      ],
      questions: [
        {
          question:
            "If the transformation depicted in organelle B requires oxygen, what form of energy is represented by E IV?",
          ansA: "Radiant energy in the form of photons",
          ansB: "Chemical energy being stored as glycogen",
          ansC: "Chemical energy in the form of ATP",
          ansD: "Chemical energy released by glycolysis",
          answer: "A",
        },
      ],
      a: 0,
      b: 1,
      index: 0,
      score: 0,
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
      this.index++;
    },
    prevQuestion() {
      this.a--;
      this.b--;
      this.index--;
    },
    checkCorrect(answer) {
      console.log(this.index);
      console.log(answer);
      console.log(this.questions[this.index].answer);
      if (answer === this.questions[0].answer) {
        console.log("Correct");
      } else {
        console.log("Incorrect");
      }
    },
    addQuiz() {
      let Math = [];
      this.testArray.push({ Math });
      console.log(this.testArray);
    },
    testHandle() {
      this.testArray[0].test1.push({ question: "hello", reponse: "goodbye" });
      this.testArray[0].test2.push({ question: "goodbye", reponse: "hello" });
      console.log(this.testArray[0].test1[0]);
      console.log(this.testArray[0].test2[0]);
    },
    testScore() {
      this.score = this.score + 100;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Gochi+Hand&family=Source+Sans+3&display=swap");
.title h1 {
  color: white;
}
.overCont {
  display: flex;
  justify-content: center;
  margin: 15px;
}
.container {
  width: 450px;
  font-family: "Source Sans 3";
  padding: 20px;
  background: #33628a;
  border-radius: 10px;
}
.btnContainer {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  border-radius: 10px;
}
.btnBackground button {
  background: orange;
  border: none;
  color: white;
  padding: 10px;
  padding-left: 30px;
  padding-right: 30px;
  border-radius: 25px;
  font-size: 20px;
}
.infoHead {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  text-align: left;
  padding: 10px;
  background: white;
  margin-bottom: 10px;
  border-radius: 10px;
}
.infoHead h2 {
  margin: 0px;
}
.quesContainer {
  background: white;
  padding: 10px;
  border-radius: 10px;
  margin-bottom: 20px;
}
.question {
  display: flex;
  flex-direction: column;
  height: 425px;
  justify-content: space-between;
}
.quesTitle {
  text-align: left;
  padding: 15px;
}
.quesTitle p {
  font-size: 20px;
  margin: 0px;
}
.choiceCont {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.choice {
  border-radius: 15px;
  width: 400px;
  margin: 10px;
  background: #d9e2e9;
}
.choice p {
  margin: 7px;
  font-size: 18px;
}
</style>
