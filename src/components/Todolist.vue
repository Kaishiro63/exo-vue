<script>
  export default {
    name: 'Task',
    props: {
      msg: String,
    },

    data() {
      return {
        task: '',
        tasks: [],
        editIndex: null,
        availableStatuses: ['a-faire', 'en-cours', 'termine'],
      }
    },

    methods: {
      submitTask() {
        if (this.task.length === 0) return;

        if (this.editIndex !== null) {
          this.tasks[this.editIndex].name = this.task;
          this.editIndex = null;
        } else {
          this.tasks.push({
            name: this.task,
            status: 'a-faire',
          });
        }

        this.task = '';
      },

      deleteTask(index) {
        this.tasks.splice(index, 1);
      },

      editTask(index) {
        this.editIndex = index;
        this.task = this.tasks[index].name;
        this.$nextTick(() => {
          const input = document.querySelector('.input input');
          input.focus();
        });
      },

      changeStatus(index) {
        let newIndex = this.availableStatuses.indexOf(this.tasks[index].status);
        if (++newIndex > 2) newIndex = 0;
        this.tasks[index].status = this.availableStatuses[newIndex];
      }
    }
  };
</script>

<template>
  <div>
    <h1>To Do List</h1>
    <div>
      <form class="input" @submit.prevent="submitTask">
        <input v-model="task" type="text" placeholder="Entre une tache">
        <button>{{ editIndex !== null ? 'Modifier' : 'Valider' }}</button>
      </form>
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
        </ul>
        <div>
          <button @click="changeStatus(index)" :class="task.status">{{ task.status }}</button>
          <button @click="editTask(index)">Modifier<i class="fa fa-pen"></i></button>
          <button @click="deleteTask(index)">Supprimer<i class="fa fa-trash"></i></button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
  .a-faire{
    color: red;
    cursor: pointer;
    width: 140px;
  }

  .en-cours {
    color: yellow;
    cursor: pointer;
    width: 140px;
  }

  .termine {
    color: #03C04A;
    cursor: pointer;
    width: 140px;
  }
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
    max-width: 380px;
  }
  li{
    list-style: none;
    padding: 10px;
    text-align: left;
  }
  i{
    margin-right: 3px;
  }
  .status{
    cursor: pointer;
  }
</style>
