<template>
  <div id=app>
    <header>
      <h1>The Adventurer's Spellbook</h1>
      <ul v-if: spells>
        <li v-for="(spell) in this.spells" :key='spell.index'> {{spell.name}}</li>
      </ul>
    </header>
  </div>
</template>

<script>
export default {
  name:"app",
  components: {
  },
  data() {
    return {
      spells: [],
      selectedSpell: null
    };
  },
  mounted() {
    fetch("https://www.dnd5eapi.co/api/spells")
    .then(response => response.json())
    .then(spells => this.spells = spells.results);
  }
}
</script>

<style>

</style>