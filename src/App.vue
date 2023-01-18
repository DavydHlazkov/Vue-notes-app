<template>
  <main>
    <div v-if="showModal" class="overlay">
      <div class="modal">
        <textarea
          v-model="newNote"
          name="notes"
          id="notes"
          cols="30"
          rows="10"
        ></textarea>
        <button @click="addNote">Add notes</button>
        <button @click="showModal = false" class="close">Close</button>
      </div>
    </div>
    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="showModal = true">+</button>
      </header>
      <div class="cards-container">
        <div
          :style="{ backgroundColor: note.backgroundColor }"
          class="card"
          v-for="note in notes"
          :key="note.id"
        >
          <p class="main-text">
            {{ note.text }}
          </p>
          <p class="date">{{ note.date }}</p>
        </div>
      </div>
    </div>
  </main>
</template>

<script setup>
import { ref } from "vue";

const showModal = ref(false);
const notes = ref([]);
const newNote = ref("");
const getRandomColor = () => {
  return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
};

const addNote = () => {
  if (newNote.value.length >= 3) {
    notes.value.push({
      text: newNote.value,
      date:
        new Date().getDate() +
        "/" +
        new Date().getMonth() +
        "/" +
        new Date().getFullYear(),
      id: Math.floor(Math.random() * 1000000),
      backgroundColor: getRandomColor(),
    });
    newNote.value = "";
    showModal.value = false;
  }
};
</script>

<style scoped>
main {
  height: 100vh;
  width: 100vw;
}
.container {
  max-width: 1000px;
  padding: 10px;
  margin: 0 auto;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

h1 {
  font-weight: bold;
  margin-bottom: 25px;
  font-size: 75px;
  color: rgb(21, 20, 20);
}

header button {
  border: none;
  padding: 10px;
  width: 50px;
  height: 50px;
  cursor: pointer;
  background-color: rgb(21, 20, 20);
  border-radius: 100%;
  color: white;
  font-size: 20px;
}

.cards-container {
  display: flex;
  flex-wrap: wrap;
}

.card {
  width: 225px;
  height: 225px;
  background-color: rgb(237, 182, 42);
  padding: 10px;
  border-radius: 15px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-right: 20px;
  margin-bottom: 20px;
}

.date {
  font-size: 12.5px;
  font-weight: bold;
}

.overlay {
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.77);
  z-index: 10;
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal {
  width: 750px;
  background-color: white;
  border-radius: 10px;
  padding: 30px;
  position: relative;
  display: flex;
  flex-direction: column;
}

.modal button {
  padding: 10px 20px;
  font-size: 20px;
  width: 100%;
  border: none;
  color: #000;
  cursor: pointer;
  margin-top: 15px;
  background-color: rgb(128, 255, 196);
  border-radius: 7px;
}

.modal .close {
  background-color: rgb(255, 128, 128);
  margin-top: 7px;
  border-radius: 7px;
}
</style>
