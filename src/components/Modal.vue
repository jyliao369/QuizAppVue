<template>
  <div class="backdrop">
    <div class="container">
      <div class="questionForm">
        <div class="titleForm">
          <h2>Add a Question</h2>
        </div>
        <div class="qForm">
          <h3>Question</h3>
          <input class="question" v-model="title" />
        </div>
        <div class="aForm">
          <h3>Choice A</h3>
          <input class="choiceA" v-model="choiceA" />
        </div>
        <div class="bForm">
          <h3>Choice B</h3>
          <input class="choiceB" v-model="choiceB" />
        </div>
        <div class="cForm">
          <h3>Choice C</h3>
          <input class="choiceC" v-model="choiceC" />
        </div>
        <div class="dForm">
          <h3>Choice D</h3>
          <input class="choiceD" v-model="choiceD" />
        </div>
        <div class="ansForm">
          <h3>The Answer is:</h3>
          <div class="choices">
            <input
              type="radio"
              value="A"
              id="answer"
              name="answer"
              v-model="answer"
            />
            A
            <input
              type="radio"
              value="B"
              id="answer"
              name="answer"
              v-model="answer"
            />
            B
            <input
              type="radio"
              value="C"
              id="answer"
              name="answer"
              v-model="answer"
            />
            C
            <input
              type="radio"
              value="D"
              id="answer"
              name="answer"
              v-model="answer"
            />
            D
          </div>
        </div>
      </div>
      <div class="btns">
        <button @click.self="closeModal" class="canBtn">Cancel</button>
        <button @click="addQuestion" class="creBtn">Create</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: "",
      choiceA: "",
      choiceB: "",
      choiceC: "",
      choiceD: "",
      answer: "",
    };
  },
  methods: {
    closeModal() {
      this.$emit("close");
    },
    addQuestion() {
      this.$emit(
        "showQuestion",
        this.title,
        this.choiceA,
        this.choiceB,
        this.choiceC,
        this.choiceD,
        this.answer
      );
      this.$emit("close");
    },
  },
};
</script>

<style scoped>
.backdrop {
  top: 0;
  position: fixed;
  background: rgba(0, 0, 0, 0.5);
  width: 100%;
  height: 100%;
}
.container {
  width: 625px;
  padding: 30px 40px 30px 40px;
  margin: 100px auto;
  background: white;
  border-radius: 10px;
}
.container h1,
h2,
h3 {
  margin: 0px;
}
.questionForm {
  display: flex;
  flex-direction: column;
  margin-bottom: 25px;
}
.questionForm h3 {
  margin-bottom: 5px;
}
.titleForm {
  display: flex;
  align-items: flex-start;
  margin-bottom: 20px;
}
.qForm,
.aForm,
.bForm,
.cForm,
.dForm,
.ansForm {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  margin-bottom: 20px;
}
.ansForm {
  display: flex;
  flex-direction: column;
}
.choices {
  display: flex;
  flex-direction: row;
  align-items: flex-start;
}
.question,
.choiceA,
.choiceB,
.choiceC,
.choiceD,
.answer {
  width: 100%;
  box-sizing: border-box;
  font-size: 15px;
  padding: 10px;
  border-radius: 5px;
}
.btns {
  display: flex;
  justify-content: right;
}
.btns .canBtn {
  border-radius: 5px;
  background: #d9d9d9;
  font-size: 20px;
  padding: 10px;
  border-width: 2px;
  border: none;
}
.btns .creBtn {
  border-radius: 5px;
  background: green;
  margin-left: 24px;
  color: white;
  border: none;
  font-size: 20px;
  padding: 10px;
}
</style>
