<template>
  <div id=app>
    <header>
      <h1>The Adventurer's Spellbook</h1>
      <spell-list :spells="spells">
        
      </spell-list>
    </header>
  </div>
</template>

<script>
import SpellList from "@/components/spellList";
export default {
  name:"app",
  components: {
    "spell-list": SpellList
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