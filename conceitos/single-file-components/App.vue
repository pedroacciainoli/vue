<script>
export default{
  data: () => ({
    name: 'Igor',
    link: 'https://google.com'
  })

}

</script>

<template>
  <div>
    <h1>
      Hello {{name}}
      <input type="text" v-model="name">
    </h1>
    <a :href="link">Link </a>
  </div>
</template>

<style>

</style>