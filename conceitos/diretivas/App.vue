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
  })
}
</script>

<template>
  <div>
    <h1>
      Tarefas
    </h1>
    <button @click="() => showList = !showList">
      Ver Lista
    </button>
    <br/>
    <input type="text" v-focus>
    <ul v-if="showList">
      <li
          v-for="(task, index) in tasks"
          :key="`${task}-${index}`"
      >
        {{task.name}}
      </li>
    </ul>
    <p v-else>
      Lista Escondida
    </p>
  </div>
</template>

<style>

</style>