<script setup>
import { ref } from "vue";
import VueFrather from "vue-feather";

const newTodo = ref("");
const todo = ref([]);
const crossedOut = ref(false);
const errorMessage = ref("");

function todoView() {
  if (newTodo.value.length < 2) {
    return (errorMessage.value = "Todos cannot be empty or single character ");
  }
  todo.value.push({
    id: Math.floor(Math.random() * 1000000),
    text: newTodo.value,
  });
  errorMessage.value = "";
  this.newTodo = ""; // to clear the model from the input
  // todo = [];
}
</script>

<template>
  <main>
    <div class="container">
      <h1>ToDo</h1>
    </div>
    <div class="textArea">
      <input v-model="newTodo" type="text" ref="todoo" />

      <button @click="todoView()" class="btn">+</button>
    </div>
    <div class="error-caontainer">
      <p v-if="errorMessage">{{ errorMessage }}</p>
    </div>

    <div class="cardContainer">
      <div v-for="todos in todo" class="card">
        <p :class="{ 'crossed-out': todos.crossedOut }">
          {{ todos.text }}
        </p>
        <button @click="todos.crossedOut = !crossedOut">x</button>
      </div>
    </div>
  </main>
</template>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Konkhmer+Sleokchher&display=swap");

h1 {
  font-family: cursive;
  font-size: xx-large;
  color: #537188;
}
main {
  height: 100vh;
  width: 100vw;
}
.container {
  max-width: 1000px;
  padding: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 0 auto;
}
.btn {
  width: 50px;
  height: 50px;
  border-radius: 50px;
  background-color: #537188;
  border: 0;
  color: aliceblue;
  cursor: pointer;
  margin-left: 20px;
}
.textArea {
  display: flex;
  justify-content: center;
  margin-top: 20px;
}
.textArea input {
  width: 400px;
  height: 50px;
  font-size: x-large;
  border-color: #537188;
  border-width: 2px;
}
.cardContainer {
  display: flex;
  flex-wrap: wrap;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  margin-top: 50px;
}
.card {
  width: 400px;
  height: 50px;

  display: flex;
  flex-direction: row;
  justify-content: space-between;
  margin-top: 20px;
  padding-left: 10px;
  margin-left: -70px;
}
.card p {
  color: white;
  font-size: xx-large;
  margin-top: 0;
  color: #537188;
}
.card button {
  height: 40px;
  width: 30px;
  font-weight: bolder;
}
.crossed-out {
  text-decoration: line-through;
}
.error-caontainer {
  display: flex;
  justify-content: center;
}
.error-caontainer p {
  color: red;
  font-weight: bold;
}
</style>
