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
import { eventBus } from "@/main.js"
import SpellList from "@/components/spellList";
export default {
  name:"app",
  components: {
    "spell-list": SpellList
  },
  data() {
    return {
      rawSpells:[],
      spells: [],
      selectedSpell: null
    };
  },
  methods: {
    getRawSpells: function() {
      fetch("https://www.dnd5eapi.co/api/spells")
      .then(response => response.json())
      .then(spells => this.rawSpells = spells.results)
      .then (() => this.getDetailedSpells());
    },

    getDetailedSpells: function() {
      for (const spell of this.rawSpells) {
        fetch(`https://www.dnd5eapi.co${spell.url}`)
        .then(response => response.json())
        .then(data => this.spells.push(data))
      }
    }
      
  },

  mounted() {
    this.getRawSpells()

    eventBus.$on("spell-selected", spell => (this.selectedSpell = spell));
  }
}
</script>

<style>

</style>