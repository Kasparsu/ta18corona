<template>
  <div class="columns is-multiline is-mobile">
    <div class="column is-one-fifth">
      <stats :data="world"></stats>
    </div>
    <div class="column is-one-fifth" v-for="country in countries" >
      <stats :data="country"></stats>
    </div>
  </div>
</template>

<script>
    import Stats from "./Stats";
    export default {
        name: "StatsList",
      components: {Stats},
      props: ['countries', 'world']
    }
</script>

<style scoped>

</style>
