<template>
  <div id="app" class="container">
    <h1 class="title">To-Do List Application</h1>

    <div class="grid-layout">
      <!-- To-Do List -->
      <div class="section to-dolist">
        <h2 class="section-title">To-Do List</h2>
        <input v-model="newTask" class="input-task" placeholder="Add a new task" @keyup.enter="addTask">
        <ul class="task-list">
          <li v-for="(task, index) in tasks" :key="index" class="task-item">
            {{ task }}
            <button @click="removeTask(index)" class="button-remove">Remove</button>
          </li>
        </ul>
      </div>

      <!-- Click Counter -->
      <div class="section">
        <h2 class="section-title">Click Counter</h2>
        <button @click="counter++" class="button-counter">You clicked me {{ counter }} times</button>
      </div>

      <!-- Box Color Changer -->
      <div class="section">
        <h2 class="section-title">Box Color Changer</h2>
        <div class="box" :style="{ backgroundColor: currentColor }"></div>
        <div class="buttons">
          <button @click="changeColor('red')" class="button-color">Red</button>
          <button @click="changeColor('green')" class="button-color">Green</button>
          <button @click="changeColor('blue')" class="button-color">Blue</button>
        </div>
      </div>

      <!-- Image Carousel -->
      <div class="section">
        <h2 class="section-title">Image Carousel</h2>
        <div class="carousel">
          <button @click="prevImage" class="button-carousel">&lt;</button>
          <img :src="images[currentImage]" alt="Carousel Image" class="carousel-image">
          <button @click="nextImage" class="button-carousel">&gt;</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // To-Do List
      newTask: '',
      tasks: [],

      // Click counter
      counter: 0,

      // Color changer
      currentColor: 'white',

      // Image carousel
      images: [
        // require('@/assets/gambar1.jpg'), // Gambar pertama
        // require('@/assets/gambar2.jpg'), // Gambar kedua
        // require('@/assets/gambar3.jpg')  // Gambar ketiga
      ],
      currentImage: 0
    };
  },
  created() {
    // Load tasks from localStorage if available
    const savedTasks = localStorage.getItem('tasks');
    if (savedTasks) {
      this.tasks = JSON.parse(savedTasks);
    }
  },
  watch: {
    // Watch for changes in tasks and save them to localStorage
    tasks: {
      handler(newTasks) {
        localStorage.setItem('tasks', JSON.stringify(newTasks));
      },
      deep: true
    }
  },
  methods: {
    // To-Do List Methods
    addTask() {
      if (this.newTask !== '') {
        this.tasks.push(this.newTask);
        this.newTask = '';
      }
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
    },

    // Method to change the box color
    changeColor(color) {
      this.currentColor = color;
    },

    // Methods for image carousel
    nextImage() {
      this.currentImage = (this.currentImage + 1) % this.images.length;
    },
    prevImage() {
      this.currentImage = (this.currentImage - 1 + this.images.length) % this.images.length;
    }
  }
};
</script>

<style scoped>
/* Global Styles */
.container {
  max-width: 900px;
  margin: 0 auto;
  padding: 20px;
  font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
  background-color: #6482ad;
  border-radius: 10px;
}

.title {
  text-align: center;
  margin-bottom: 30px;
  color: black;
  font-weight: bold;
}

.grid-layout {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
}

/* Section Styles */
.section {
  padding: 20px;
  background-color: #7fa1c3;
  border-radius: 10px;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
}

.section-title {
  text-align: center;
  margin-bottom: 15px;
  font-size: 1.5em;
  color: black;
}

/* To-Do List Styles */
.input-task {
  width: 100%;
  padding: 10px;
  margin-bottom: 15px;
  border: 2px solid black;
  border-radius: 6px;
  box-sizing: border-box;
}

.task-list {
  list-style: none;
  padding: 0;
}

.task-item {
  padding: 10px;
  margin-bottom: 10px;
  background-color: #e2dad6;
  color: black;
  border-radius: 6px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
}

.button-remove {
  background-color: red;
  color: white;
  border: none;
  padding: 5px 12px;
  border-radius: 4px;
  cursor: pointer;
}

.button-remove:hover {
  background-color: orange;
}

/* Click Counter Styles */
.button-counter {
  padding: 12px 24px;
  background-color: #405d72;
  color: white;
  border: 2px solid black;
  border-radius: 6px;
  cursor: pointer;
  width: 100%;
}

.button-counter:hover {
  background-color: #758694;
}

/* Box Color Changer Styles */
.box {
  width: 120px;
  height: 120px;
  margin: 10px auto;
  border: 2px solid black;
  border-radius: 8px;
  background-color: white;
}

.buttons {
  display: flex;
  justify-content: center;
  margin-top: 10px;
}

.button-color {
  padding: 10px 20px;
  margin: 0 5px;
  border: none;
  border-radius: 6px;
  cursor: pointer;
}

.button-color:nth-child(1) {
  background-color: red;
  color: white;
}

.button-color:nth-child(2) {
  background-color: green;
  color: white;
}

.button-color:nth-child(3) {
  background-color: blue;
  color: white;
}

/* Image Carousel Styles */
.carousel {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
}

.carousel-image {
  max-width: 100%;
  height: auto;
  border: 2px solid black;
  border-radius: 5px;
}

.button-carousel {
  padding: 12px;
  background-color: #405d72;
  color: white;
  border: 1px solid black;;
  border-radius: 6px;
  cursor: pointer;
}

.button-carousel:hover {
  background-color: #758694;
}
</style>
