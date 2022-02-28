<template>
  <div v-if="showQuestionModal">
    <QuestionModal
      :categories="categories"
      @close="addQuestModal"
      @addQuestion="addQuestion"
    />
  </div>

  <div v-if="showCategoryModal">
    <CategoryModal @close="addCatModal" @addCategory="addCategory" />
  </div>
  <div class="title"><h1>Quizly</h1></div>

  <div class="overCont">
    <div class="container">
      <!-- THIS IS THE INFO HEADER -->
      <div v-if="showQuiz">
        <div class="infoHead">
          <div>
            <h2>Current Category:</h2>
          </div>
          <div>
            <h2>{{ currentCategory[0].name }}</h2>
          </div>
        </div>

        <!-- THIS IS THE SCORE HEADER -->
        <div class="infoHead">
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
            v-for="(questions, index) in currentCategory[0].questions.slice(
              a,
              b
            )"
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

          <!-- THIS IS THE BUTTON SECTION -->
          <div class="btnContainer">
            <div class="btnBackground">
              <button
                v-if="this.b === 1"
                :disabled="true"
                @click="prevQuestion"
              >
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
              <button v-else :disabled="true" @click="prevQuestion">
                Next
              </button>
            </div>
          </div>
        </div>

        <!-- RETURN BUTTON -->
        <div class="returnCon">
          <button @click="returnCat">Return</button>
        </div>
      </div>

      <div v-if="showCat">
        <div class="overCatCon">
          <!-- THIS HOLDS THE BUTTONS TO ADD NEW QUESTIONS AND CATEGORIES -->
          <div class="addQuestCatCon">
            <button @click="addCatModal">Add Category</button>
            <button @click="addQuestModal">Add Question</button>
          </div>

          <!-- THIS IS HOLDS ALL OF THE CATEGORIES  -->
          <div class="catContainer">
            <button
              v-for="(category, index) in categories"
              :key="index"
              @click="changeCategory(index)"
            >
              {{ category.name }}
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import CategoryModal from "./CategoryModal.vue";
import QuestionModal from "./QuestionModal.vue";

export default {
  components: {
    CategoryModal,
    QuestionModal,
  },
  data() {
    return {
      showQuestionModal: false,
      showCategoryModal: false,
      a: 0,
      b: 1,
      index: 0,
      score: 0,
      showQuiz: false,
      showCat: true,
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
        {
          name: "Org. Chemistry",
          questions: [],
        },
        {
          name: "Trigonmetry",
          questions: [],
        },
        {
          name: "Social Studies",
          questions: [],
        },
        {
          name: "Game Trivia",
          questions: [],
        },
        {
          name: "Geography",
          questions: [],
        },
        {
          name: "Television",
          questions: [],
        },
        {
          name: "Harry Potter",
          questions: [],
        },
      ],
    };
  },
  methods: {
    addQuestModal() {
      this.showQuestionModal = !this.showQuestionModal;
    },
    addCatModal() {
      this.showCategoryModal = !this.showCategoryModal;
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
    changeCategory(number) {
      // console.log("index value");
      // console.log(number);
      this.currentCategory = [];
      this.currentCategory.push(this.categories[number]);
      this.a = 0;
      this.b = 1;
      this.score = 0;
      this.showQuiz = !this.showQuiz;
      this.showCat = !this.showCat;
    },
    addQuestion(question, choiceA, choiceB, choiceC, choiceD, answer, index) {
      this.categories[index].questions.push({
        question: question,
        ansA: choiceA,
        ansB: choiceB,
        ansC: choiceC,
        ansD: choiceD,
        answer: answer,
      });
      // console.log(this.categories[index].questions);
    },
    addCategory(category) {
      this.categories.push({ name: category, questions: [] });
    },
    returnCat() {
      this.showQuiz = !this.showQuiz;
      this.showCat = !this.showCat;
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
  width: 500px;
  font-family: "Source Sans 3";
  padding: 15px;
  background: #33628a;
  border-radius: 10px;
}
.btnContainer {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  margin-top: 10px;
}
.btnBackground button {
  background: #ff7b7b;
  border: none;
  color: white;
  padding: 10px;
  border-radius: 25px;
  font-size: 20px;
  width: 115px;
  display: flex;
  justify-content: center;
}
.returnCon {
  display: flex;
  justify-content: center;
}
.returnCon button {
  background: orange;
  border: none;
  color: white;
  padding: 10px;
  border-radius: 25px;
  font-size: 20px;
  width: 115px;
  display: flex;
  justify-content: center;
}
.infoHead {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  text-align: left;
  padding: 10px;
  background: white;
  margin-bottom: 15px;
  border-radius: 10px;
}
.infoHead h2 {
  margin: 0px;
}
.quesContainer {
  background: white;
  padding: 10px;
  border-radius: 10px;
  margin-bottom: 15px;
}
.question {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  min-height: 450px;
}
.quesTitle {
  display: flex;
  text-align: left;
  padding: 10px;
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
  width: 100%;
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
.overCatCon {
  display: flex;
  flex-direction: column;
  background: white;
  border-radius: 15px;
  padding: 10px;
}
.addQuestCatCon {
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
  margin-bottom: 10px;
}
.addQuestCatCon button {
  background: orange;
  border: none;
  color: white;
  padding: 10px;
  border-radius: 25px;
  font-size: 15px;
  width: 185px;
  display: flex;
  justify-content: center;
}
.catContainer {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: space-between;
  font-family: "Source Sans 3";
}
.catContainer button {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 215px;
  height: 50px;
  font-size: 20px;
  border-radius: 15px;
  padding: 10px;
  border: none;
  background: #c2d0dc;
  color: #3f3f3f;
  margin: 10px;
}
</style>
