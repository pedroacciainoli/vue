
<template>
  <div>
    <h1>My todo list</h1>
    <button @click="handleShowHideList">Show the list!</button>
    <br />
    <input
        type="text"
        @keyup.enter="handleAddTask"
        v-focus
        v-model="state.currentTask"
    />
    <ul v-if="state.showList">
      <li
          v-for="(task, index) in state.tasks"
          :key="`${task}-${index}`"
          @dblclick="handleComplete(task)"
          class="task-item"
          :class="{
       'line-through': task.isDone
     }"
      >
        {{ task.name }}
        <button
            @click="handleRemove(task)"
        >
          &times;
        </button>
      </li>
    </ul>
    <p v-else>
      Todo list is hide!
    </p>
  </div>
</template>

<script>
import {reactive} from "vue";

const focus = {
  inserted: (el) => {
    el.focus()
  }
}
export default {
  directives: {
    focus,
  },
  setup(){
  const state = reactive(
      {
        showList: false,
        currentTask: '',
        tasks: [
          {name: 'Fazer o curso', isDone: false}
        ]
      }
  )
  function handleShowHideList()
{
  state.showList = !state.showList
}

function handleAddTask() {
  state.tasks.push({name: state.currentTask, isDone: false})
  state.currentTask = ''
}

function handleRemove(task) {
  state.tasks = state.tasks.filter(t => t.name !== task.name)
}

function handleComplete(task) {
  state.tasks = state.tasks.map(t => {
    if (t.name === task.name) {
      return {...t, isDone: !t.isDone}
    }
    return {...t}
  })
}

return {
  state,
  handleShowHideList,
  handleAddTask,
  handleRemove,
  handleComplete
}
}
}
</script>

<style scoped>
.line-through {
  text-decoration: line-through;
}
.task-item {
  cursor: pointer;
}
</style>