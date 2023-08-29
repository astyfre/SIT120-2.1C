<template>
  <link rel="stylesheet" type="text/css" href="styles.css">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Source+Code+Pro:wght@200;300;400&display=swap" rel="stylesheet">
  <div class="todo-app">
    <h1>T O D O</h1>
    <input v-model="newTask" @keyup.enter="addTask" placeholder="Enter a new todo task" class="create-item">
    <ul>
      <li v-for="(task, index) in tasks" :key="index" class="task-item" :class="{ 'alternate-bg': index % 2 === 1 }">
        <div class="item-content">
          <div class="left-content">
            <input type="checkbox" v-model="task.completed" class="checkbox">
            <span :class="{ completed: task.completed }">{{task.text}}</span>
          </div>
          <button @click="removeTask(index)">Remove</button>
        </div>
      </li>
    </ul>
  </div>
  <body>
  <footer>
    <p>&copy; 2023 To-Do Site</p>
  </footer></body>
</template>

<script>
export default {
  data(){
    return{
      newTask: '',
      tasks: []
    };
  },
  methods: {
    addTask(){
      if (this.newTask.trim() !== ''){
        this.tasks.push({
          text: this.newTask,
          completed: false
        });
        this.newTask='';
      }
    },
    removeTask(index){
      this.tasks.splice(index, 1);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
  font-family: 'Source Code Pro', monospace;
  font-size: 3vw;
}
footer{
  background-color: lightblue;
  color: white;
  text-align: center;
  position: fixed;
  padding: 10px 10px;
  bottom: 0px;
  width: 100%
}
.todo-app{
  max-width: 500px;
  margin: 0 auto;
  text-align: center;
  font-family: Arial, sans-serif;
  /* Apply background color and padding to create a box */
  background-color: #e9e8e8;
  padding: 20px;
  box-shadow: 0px 0px 10px 5px rgb(162, 190, 199);
}

ul {
  list-style-type: none;
  padding: 0px;
  background-color: lightblue;
}

li {
  display: flex; /* Use flexbox to align items */
  align-items: center;
  justify-content: space-between; /* Spread items across the row */
  margin: 0px 0px; /* Adjust margin for vertical spacing */
  padding: 10px; /* Add padding for space around the list items */
  font-family: 'Source Code Pro' monospace;
  font-weight: bold;
}
.create-item {
  padding: 10px;
  border: none;
  border-bottom: 2px solid rgb(141, 3, 3); /* Add a bottom border */
  font-size: 16px;
  width: 100%;
  box-sizing: border-box; /* Include padding and border in width calculation */
  transition: border-color 0.2s ease; /* Add transition effect */
}
/* Apply different background color for alternate list items */
.alternate-bg {
  background-color: #ffffff;
}

.left-content {
  display: flex; /* Align checkbox and text in a row */
  align-items: center; /* Vertically center checkbox and text */
}

.completed{
  text-decoration: line-through;
  color: #6e6e6e;
}

button {
  padding: 5px 10px;
  background-color: red;
  border: none;
  color: white;
  cursor: pointer;
  float: right;
}
button:active {
  background-color: darkred; 
}

.checkbox {
  appearance: none;
  -webkit-appearance: none;
  width: 20px;
  height: 20px;
  border: 2px solid rgb(141, 3, 3);
  background-color: white;
  border-radius: 50%;
  cursor: pointer;
  margin-right: 10px;
  position: relative;
}

.checkbox:checked {
  background-color: #007bff;
}

.checkbox:before {
  content: '\2713'; /* Checkmark symbol */
  position: absolute;
  top: 50%; /* Center vertically */
  left: 50%; /* Center horizontally */
  transform: translate(-50%, -50%); /* Center the checkmark */
  font-size: 14px;
  font-weight: bold;
  color: white;
  opacity: 0;
  transition: opacity 0.2s ease;
}

.checkbox:checked:before {
  opacity: 1;
}

@media screen and (max-width: 900px) {
  
  .task-item {
    text-align: center; /* Center the content horizontally */
    display: flex; /* Use flexbox for vertical centering */
    flex-direction: column; /* Stack elements vertically */
    justify-content: center; /* Center items vertically */
    align-items: center; /* Center items horizontally */
  }
  

  .item-content button {
    margin-top: 10px; /* Add some spacing between items */
  }
  button {
  padding: 10px 50px;
}
}

/* Media query for larger screens */
@media screen and (min-width: 901px) {
  .item-content {
    display: flex; /* Align items in a row */
    justify-content: space-between; /* Place items at both ends horizontally */
    align-items: center; /* Center vertically */
    width: 100%; /* Ensure the content stretches across the item */
  }
  
}
</style>
