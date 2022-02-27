<template>
  <div class="backdrop">
    <div class="container">
      <div class="categoryForm">
        <div class="titleForm">
          <h2>Add a New Category</h2>
        </div>
        <div class="catForm">
          <h3>Name of New Category</h3>
          <input class="category" v-model="category" />
        </div>
        <div class="btns">
          <button @click.self="closeModal" class="canBtn">Cancel</button>
          <button @click="addCategory" class="creBtn">Add Category</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      category: "",
    };
  },
  methods: {
    closeModal() {
      this.$emit("close");
    },
    addCategory() {
      this.$emit("addCategory", this.category);
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
  width: 550px;
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
.categoryForm h3 {
  margin-bottom: 5px;
}
.titleForm {
  display: flex;
  align-items: flex-start;
  margin-bottom: 20px;
}
.catForm {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  margin-bottom: 20px;
}
.category {
  width: 100%;
  box-sizing: border-box;
  font-size: 20px;
  padding: 10px;
  border-radius: 5px;
}
.btns {
  display: flex;
  justify-content: right;
}
.canBtn {
  border-radius: 5px;
  background: #d9d9d9;
  font-size: 20px;
  padding: 10px;
  border-width: 2px;
  border: none;
}
.creBtn {
  border-radius: 5px;
  background: green;
  margin-left: 24px;
  color: white;
  border: none;
  font-size: 20px;
  padding: 10px;
}
</style>
