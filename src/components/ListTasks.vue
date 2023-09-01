<template>
  <header> 
    <h1 class="title">Todo</h1>
    <img alt="Vue logo" src="../assets/logo.png">
  </header>
  
  <div class="inputTaskContainer"> 
    <input v-model="newTask" class="inputTask" type="Text" placeholder="Adicione uma nova tarefa">
    <button v-on:click="getTask()">Criar</button>
  </div>
  
  <ul class="listTasks">
    
    <div class="taskInfo">
      <div class="count">
        <span>Tarefas Criadas</span>
        <span class="countLength">{{ listTasks.length }}</span>
      </div>
      <div class="executedTaskCounter count">
        <span>Concluídas</span>
        <span class="countLength">{{countCompletedTasks()}} de {{ listTasks.length }}</span>
      </div>
    </div>
    
    <li v-for="task in listTasks" :key="task.id"> 
      <input type="checkbox" class="buttonDone" v-model="task.done" @change="updateTaskCompletion(task)" />
      <p :class="{'done': task.done}">{{ task.task }}</p> 
      <button class="buttonDelete" v-on:click="deleteTask(task)">
        <svg xmlns="http://www.w3.org/2000/svg" x="0px" y="0px" viewBox="0,0,256,256">
          <g fill="#757575" fill-rule="nonzero" stroke="none" stroke-width="1" stroke-linecap="butt" stroke-linejoin="miter" stroke-miterlimit="10" stroke-dasharray="" stroke-dashoffset="0" font-family="none" font-weight="none" font-size="none" text-anchor="none" style="mix-blend-mode: normal"><g transform="scale(2,2)"><path d="M49,1c-1.66,0 -3,1.34 -3,3c0,1.66 1.34,3 3,3h30c1.66,0 3,-1.34 3,-3c0,-1.66 -1.34,-3 -3,-3zM24,15c-7.17,0 -13,5.83 -13,13c0,7.17 5.83,13 13,13h77v63c0,9.37 -7.63,17 -17,17h-40c-9.37,0 -17,-7.63 -17,-17v-52c0,-1.66 -1.34,-3 -3,-3c-1.66,0 -3,1.34 -3,3v52c0,12.68 10.32,23 23,23h40c12.68,0 23,-10.32 23,-23v-63.35937c5.72,-1.36 10,-6.50062 10,-12.64062c0,-7.17 -5.83,-13 -13,-13zM24,21h80c3.86,0 7,3.14 7,7c0,3.86 -3.14,7 -7,7h-80c-3.86,0 -7,-3.14 -7,-7c0,-3.86 3.14,-7 7,-7zM50,55c-1.66,0 -3,1.34 -3,3v46c0,1.66 1.34,3 3,3c1.66,0 3,-1.34 3,-3v-46c0,-1.66 -1.34,-3 -3,-3zM78,55c-1.66,0 -3,1.34 -3,3v46c0,1.66 1.34,3 3,3c1.66,0 3,-1.34 3,-3v-46c0,-1.66 -1.34,-3 -3,-3z"></path></g></g>
        </svg>
    </button>
    </li>
    <h2 class="emptyTask" v-if="listTasks.length === 0">A lista de tarefas está vazia</h2>
  </ul>
  
</template>

<script lang="ts">
import { defineComponent } from 'vue';

interface Task {
  id: number;
  task: string;
  done: boolean;
}

export default defineComponent({
  data() {
  return {
    listTasks: [
      {id: 1, task: "Organizar uma videoconferência de equipe para discutir o progresso do projeto e definir metas para a próxima semana.", done: true},
      {id: 2, task: "Realizar uma revisão de carreira, atualizando o currículo e estabelecendo metas de desenvolvimento profissional", done: false},
      {id: 3, task: "Fazer um estudo aprofundado sobre um tópico de interesse acadêmico.", done: false}
    ],
    newTask: ''
  }
 },
 methods: {
     getTask() {
        const tasknew = {id: this.listTasks.length + 1, task: this.newTask, done: false};
          if(tasknew.task){
            this.listTasks.push(tasknew)
            this.newTask = '';
          }
          
     },

     deleteTask(taskToDelete: { id: number; task: string }) {
      const taskIdToDelete = taskToDelete.id;
      const taskIndex = this.listTasks.findIndex(task => task.id === taskIdToDelete);
      if (taskIndex !== -1) {
        this.listTasks.splice(taskIndex, 1);
      }
    },

    updateTaskCompletion(task: Task) {
      let taskDone = task.done
      taskDone = !task.done;

      this.countCompletedTasks();
    },

    countCompletedTasks(){
      const completedTasks = this.listTasks.filter(task => task.done === true);
      return completedTasks.length;
    }
 },

});

</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  header {
    display: flex;
    justify-content: center;
    align-items: center;
    color: white;
    font-size: 2rem;
  }
  header img {
    width: 3rem;
  }
  .inputTaskContainer{
    display: flex;
    justify-content: center;
    align-items: center;
    width: 50%;
    gap: 0.5rem;
  }
  .inputTask {
    padding: 1rem;
    border-radius: 0.5rem;
    border: 0;
    flex: 1;
    background: #353535;
    color: white
  }

  .inputTask:focus, .inputTaskContainer button:focus{
    outline: 1px solid #555555;;
  }

  .inputTaskContainer button{
    padding: 1rem;
    border-radius: 0.5rem;
    border: 0;
    background: #41B883;
    color: white;
    cursor: pointer;
  }

  .inputTaskContainer button:hover{
    background-color: #30825d;
  }

  .listTasks{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 0.5rem;
    padding: 0;
    padding-top: 1rem;

    width: 50%;
    border-top: 1px solid #353535;
    border-radius: 0.3rem;
    
  }

  .count {
    color: #41B883;
    font-weight: 700;
    display: flex;
    align-items: center;
    gap: 0.5rem;
    width: 100%;
  }
  .taskInfo {
    width: 100%;
    display: flex;
  }
  .countLength {
    background-color: #353535;
    color: white;
    font-weight: normal;
    border-radius: 1rem;
    padding: 3px 9px;
    border-radius: 999px;
  }

  .executedTaskCounter {
    display: flex;
    justify-content: flex-end;
  }

  .listTasks li {
    display: flex;
    align-items: center;
    color: white;
    list-style: none;
    background: #353535;
    border-radius: 0.5rem;
    width: 100%;
    padding: 1rem;
    text-align: start;
    gap: 1rem;
    line-break: anywhere;
  }
  .listTasks li > p {
    width: 90%;
  }

  .buttonDelete{
    background: transparent;
    border: 0;
    border-radius: 0.5rem;
    height: 2rem;
    cursor: pointer;
  }

  .buttonDelete svg {
    width: 1.2rem; 
    height:1.2rem;
    padding: 0;
  }
  .buttonDelete svg:hover g {
    fill: rgb(255, 66, 66);
  }
  .done {
    text-decoration: line-through; 
    color: #555555;
  }
  .emptyTask{
    color: #555555;
  }

  input[type=checkbox] {
  position: relative;
  cursor: pointer;
}

input[type=checkbox]:before {
  content: "";
  display: block;
  position: absolute;
  width: 1.2rem;
  height: 1.2rem;
  right: -0.2rem;
  background-color: #353535;
  outline: 1px solid #41B883;
  border-radius: 1rem;
}

input[type=checkbox]:checked:after {
  content: " ✓ ";
  display: flex;
  justify-content: center;
  width: 1.2rem;
  height: 1.2rem;
  position: absolute;
  background-color: #41B883;
  border-radius: 1rem;
  color: white;
  right: -0.2rem;
}

@media (max-width: 600px) {
  .listTasks, .inputTaskContainer {
    width: 100%;
  }
}

</style>
