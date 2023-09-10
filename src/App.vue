/* eslint-disable*/
<template>
  <div class="app">
    <div class="container">
      <h1>To-Do List</h1>
      <p>press enter to input your task</p>

    <input type="text" v-model="newTask" @keyup.enter="addTask" placeholder="Add a new task">

    <ul>
      <li v-for="task in  tasks " :key="task.id">
        <p :class="task.isFinished ? 'strike': '' ">{{ task.text }} </p>

        <div>
          <button @click="finishTask(task.id)" class="success">Done</button>
        <button @click="removeTask(task.id)" class="danger">Delete</button>
        </div>

      </li>
    </ul>
    </div>
    
  </div>
</template>

<script>
export default {
  data() {
    return {
      tasks: [],
      newTask: "",
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== "") {
        this.tasks.push({ id: Date.now(), text: this.newTask, isFinished: false });
        this.newTask = "";
      }
    },
    removeTask(id) {
      this.tasks = this.tasks.filter(task => task.id !== id);
    },
    finishTask(id) {
      for (let i = 0; i < this.tasks.length; i++) {
        
      if(id === this.tasks[i].id){
        this.tasks[i].isFinished = true;
      }
      }
    }
  },
};
</script>

<style>
*{
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  font-family: sans-serif;
}
.app{
  display: grid;
  place-items: center;
  height: 100vh;
}
p{
  margin-top: -10px;
}
.container{
  display: grid;
  place-items: center;
  gap: 20px;
}
.container input{
  width: 400px;
  height: 45px;
  padding-left: 10px;
  border-top: none;
  border-bottom: 2px solid #000;
  border-right: none;
  border-left: none;
}
ul li p{
  font-size: 18px;
}

ul{
  box-shadow: 0 0 3px 0 #808080;
  padding: 10px;
  border-radius: 20px;
}
ul li{
  width: 90%;
  margin-left: 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
ul li button{
  border: none;
  padding: 10px 15px;
  border-radius: 5px;
  cursor: pointer;
}

ul li .success{
  margin-right: 10px;
  background: rgb(107, 255, 107);
}
ul li .danger{
  background: rgb(245, 74, 74);
  color: #fff;
}

.strike {
  text-decoration: line-through;
  color: rgb(90, 92, 90);
}

@media screen and (max-width:699px) {
  .container input{
    width: 300px;
  }
  ul{
    padding-top: 30px;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;    
  }
  ul li{
    display: grid;
    place-items: start;
    width: 100%;
    margin-bottom: 27px;
  }
  ul li button{
    margin-top: 10px;
  }
}
@media screen and (min-width:700px) {
  .container
  .container input{
    width: 500px;
  }
 ul{
    padding-top: 30px;
    /* width: 500px; */
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-direction: column; 
    padding-right: 25px;   
  }
  
  ul li{
    width: 100%;
    margin-bottom: 27px;
  } 
} 
</style>
