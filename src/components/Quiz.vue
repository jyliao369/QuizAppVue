<template>
  <div v-if="showModal">
    <Modal @close="addQuestion" @showQuestion="showQuestion" />
  </div>
  <div class="title"><h1>Quizly</h1></div>

  <div class="addQues">
    <!-- <button @click="addQuiz">Add New Quiz</button> -->
    <button @click="addQuestion">Add Question</button>
    <button @click="addCategory">Add New Category</button>
    <!-- <button @click="addQuiz">test</button> -->
  </div>

  <div class="overCont">
    <div class="container">
      <!-- THIS IS THE SCOPRE SECTION -->
      <div class="infoHead">
        <div>
          <h2>{{ currentCategory[0].name }}</h2>
        </div>
        <div>
          <h2>
            Question {{ b }}/{{ this.currentCategory[0].questions.length }}
          </h2>
        </div>
        <div>
          <h2>Score: {{ score }}</h2>
        </div>
      </div>
      <!-- THIS IS THE QUESTION AND ANSWER SECTION -->
      <div class="quesContainer">
        <div
          class="question"
          v-for="(questions, index) in currentCategory[0].questions.slice(a, b)"
          :key="index"
        >
          <div class="quesTitle">
            <p>{{ questions.question }}</p>
          </div>
          <div class="choiceCont">
            <div class="choice">
              <p @click="checkCorrect('A')">A: {{ questions.ansA }}</p>
            </div>
            <div class="choice">
              <p @click="checkCorrect('B')">B: {{ questions.ansB }}</p>
            </div>
            <div class="choice">
              <p @click="checkCorrect('C')">C: {{ questions.ansC }}</p>
            </div>
            <div class="choice">
              <p @click="checkCorrect('D')">D: {{ questions.ansD }}</p>
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
            v-if="this.b <= this.currentCategory[0].questions.length - 1"
            :disabled="false"
            @click="nextQuestion"
          >
            Next
          </button>
          <button v-else :disabled="true" @click="prevQuestion">Next</button>
        </div>
      </div>
    </div>

    <!-- THIS IS HOLDS ALL OF THE CATEGORIES  -->
    <div class="catContainer">
      <div v-for="(category, index) in categories" :key="index">
        <button @click="changeCategory(index)">{{ category.name }}</button>
      </div>
    </div>
  </div>
  <br />
  <br />
  <br />
  <br />
  <br />
</template>

<script>
import Modal from "./Modal.vue";

export default {
  components: {
    Modal,
  },
  data() {
    return {
      currentCategory: [
        {
          name: "Biology",
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
      categories: [
        {
          name: "Chemistry",
          questions: [
            {
              question: "Which of the following has a positive charge?",
              ansA: "proton",
              ansB: "neutron",
              ansC: "anion",
              ansD: "electron",
              answer: "A",
            },
            {
              question:
                "Rutherford carried out experiments in which a beam of alpha particles was directed at a thin piece of metal foil. From these experiments he concluded that:",
              ansA: "electrons are massive particles.",
              ansB: "the positively charged parts of atoms are moving about with a velocity approaching the speed of light.",
              ansC: "the positively charged parts of atoms are extremely small and extremely heavy particles.",
              ansD: "the diameter of an electron is approximately equal to that of the nucleus.",
              answer: "C",
            },
          ],
        },
        {
          name: "Math",
          questions: [
            {
              question: "What is three fifth of 100?",
              ansA: "3",
              ansB: "5",
              ansC: "20",
              ansD: "60",
              answer: "D",
            },
            {
              question: "What is the remainder of 21 divided by 7?",
              ansA: "0",
              ansB: "7",
              ansC: "1",
              ansD: "21",
              answer: "A",
            },
          ],
        },
        {
          name: "Trivia",
          questions: [
            {
              question: "What is the national language of Canada?",
              ansA: "English",
              ansB: "Dutch",
              ansC: "Chinese",
              ansD: "French",
              answer: "D",
            },
            {
              question: "Saudi Arabia is the biggest producer of?",
              ansA: "Coffee",
              ansB: "Oil",
              ansC: "Coal",
              ansD: "Bread",
              answer: "B",
            },
          ],
        },
      ],
      newCategory: {
        name: "History",
        questions: [
          {
            question:
              "Which of these countries did the Soviet Union NEVER invade?",
            ansA: "Afghanistan",
            ansB: "Finland",
            ansC: "Poland",
            ansD: "Sweden",
            answer: "D",
          },
          {
            question: "Who was the first person to orbit the Earth?",
            ansA: "Neil Armstrong",
            ansB: "The Boss",
            ansC: "Yuri Gagarin",
            ansD: "John Glenn",
            answer: "C",
          },
        ],
      },
      showModal: false,
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
        this.score = this.score + 100;
      } else {
        console.log("Incorrect");
        this.score = this.score - 100;
      }
    },
    testHandle() {
      this.testArray[0].test1.push({ question: "hello", reponse: "goodbye" });
      this.testArray[0].test2.push({ question: "goodbye", reponse: "hello" });
      console.log(this.testArray[0].test1[0]);
      console.log(this.testArray[0].test2[0]);
    },
    changeCategory(number) {
      console.log("index value");
      console.log(number);
      this.currentCategory = [];
      this.currentCategory.push(this.categories[number]);
    },
    addCategory() {
      this.categories.push(this.newCategory);
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
  flex-direction: column;
  justify-content: center;
  margin: 15px;
  align-items: center;
}
.container {
  width: 450px;
  font-family: "Source Sans 3";
  padding: 20px;
  background: #33628a;
  border-radius: 10px;
  margin-bottom: 20px;
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
.choice:hover {
  background: #706eeb;
  color: white;
}
.choice p {
  margin: 7px;
  font-size: 18px;
}
.catContainer {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: space-around;
  width: 450px;
  font-family: "Source Sans 3";
  padding: 20px;
  background: #33628a;
  border-radius: 10px;
}
.catContainer button {
  width: 125px;
  font-size: 20px;
  border-radius: 15px;
  padding: 15px;
  margin: 10px;
  border: none;
  background: #c2d0dc;
  color: #3f3f3f;
}
</style>
