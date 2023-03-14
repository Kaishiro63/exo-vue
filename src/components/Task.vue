<script>
  export default {
    name: 'Task',
    props: {
      msg: String,
    },

    data(){
      return {
        task: '',
        tasks: [
          {
            name: 'ma premiere tache',
            status: 'en cours'
          },
          {
            name: 'ma deuxieme tache',
            status: 'terminé'
          }
        ]
      }
    },

    methods: {
      submitTask(){
        if (this.task.length === 0) return;

        this.tasks.push({
          name: this.task,
          status: 'en cours',
        });

        this.task = '';
      },

      deleteTask(index){
        this.tasks.splice(index, 1);
      },

      editTask(index) {
        const newName = prompt('Entrez le nouveau nom de la tâche :');
        if (newName && newName.length > 0) {
          this.tasks[index].name = newName;
        }
      },
    }
  };
</script>

<template>
  <div>
    <h1>To Do List</h1>
    <div class="input">
      <input v-model="task" type="text" placeholder="Entre une tache">
      <button @click="submitTask">Valider</button>
    </div>
  </div>
  <div>
    <div>
      <h2>Vos taches</h2>
    </div>
    <div>
      <div v-for="(task, index) in tasks" :key="index" class="row">
        <ul>
          <li>{{ task.name }}</li>
          <li>{{ task.status }}</li>
        </ul>
        <div>
          <button @click="editTask(index)">Editer<i class="fa fa-pen"></i></button>
          <button @click="deleteTask(index)">Supprimer<i class="fa fa-trash"></i></button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
  .input{
    display: flex;
    margin-bottom: 40px;
  }
  input{
    width: 100%;
    height: 40px;
  }
  .row{
    display: flex;
    align-items: center;
    justify-content: space-between;
    border-bottom: solid 1px;
  }
  ul{
    display: flex;
    margin: 0;
    padding: 12px;
    max-width: 500px;
  }
  li{
    list-style: none;
    padding: 10px;
    text-align: left;
  }
  i{
    margin-right: 3px;
  }
</style>