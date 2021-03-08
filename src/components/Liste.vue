<template>
    <div>
        <h1>{{ msg }}</h1>
        <div>
            <label for="saisie">Ajoutez votre truc à faire : </label>
            <input name="saisie" v-model="newTodo" placeholder="saisir ici">
            <button @click="addTodo()">Ajouter</button>
        </div>
        <ul>
            <li v-for="item in filteredList" v-bind:key="item.id">
                {{ item.name }}
                <input @click="complete(item.id)" type="checkbox" :name="item.id" :checked="item.completed">
                <label :for="item.id">complete</label>
                <button @click="supprimer(item.id)">Supprimer</button>
            </li>
        </ul>
        <div v-if="todos.length > 0">
            <button @click="filterTasks('tt')">Afficher uniquement les tâches terminées</button>
            <button @click="filterTasks('ct')">Afficher uniquement les tâches non terminées</button>
        </div>
        <p v-if="todos.length === 0">La liste est vide</p>
    </div>
</template>

<script>
export default {
  name: 'Liste',
  data() {
    return {
        todos: [
        {
            id: 1,
            name : 'tache 1',
            completed : false 
        },
        {
            id: 2,
            name : 'tache 2',
            completed: true
        }],
        newTodo: '',
        filter: 'all',
    }
  },
  methods: {
      filterTasks(filtre){
          return this.filter = filtre;
      },
      complete(indexItem){
          return this.todos[indexItem-1].completed = !this.todos[indexItem-1].completed;
      },
      supprimer(indexItem){
          this.todos.splice(indexItem,1);
          this.todos.forEach((item,indexItem) => {
              item.id = indexItem - 1;
          });
      },
      addTodo(){
          if(this.newTodo !== ''){
              this.todos.push({
                  id: this.todos.length+1,
                  name: this.newTodo,
                  completed: false
              });
              this.newTodo = '';
          }
      }
  },
  computed: {
      filteredList(){
          return this.todos.filter(item => {
              switch(this.filter){
                  case 'all':
                    return item;
                  case 'tt':
                    return item.completed;
                  case 'ct':
                    return !item.completed;
              }
          });
      }
  },
  props: {
    msg: String
  }
}
</script>

<style scoped>

</style>