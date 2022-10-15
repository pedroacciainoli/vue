<script>
const focus = {
  inserted: (el) => {
    el.focus()
  }
}

export default{
  directives: {
    focus
  },
  data: () => ({
    showList: false,
    tasks:[
      { name: 'Fazer curso', isDone: false }
    ]
  }),
  methods:{
    handleShowHideList (){
      this.showList = !this.showList
    },
    remove (task){
      this.tasks = this.tasks.filter(t => t.name !== task.name)
    },
    complete(task){
      this.tasks = this.tasks.map (t => {
        if(t.name === task.name){
          return {...t, isDone: !t.isDone}

        }
        console.log(this.tasks);
        return {...t}
      })
    },

  }
}
</script>

<template>
  <div>
    <h1>
      Tarefas
    </h1>
    <button @click="handleShowHideList">
      Ver Lista
    </button>

    <br/>
    <input type="text" v-focus>
    <ul v-if="showList">
      <li
          v-for="(task, index) in tasks"
          :key="`${task}-${index}`"
          @dblclick="complete"
          :class="{
          'line-through': task.isDone
          }"

      >
        {{task.name}}
        <button @click="remove(task)">
          &times
        </button>
      </li>

    </ul>

    <p v-else>
      Lista Escondida
    </p>
  </div>
</template>

<style>
.line-through{
  text-decoration: line-through;
}
</style>