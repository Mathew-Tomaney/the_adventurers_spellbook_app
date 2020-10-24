<template>
  <div id=app>
    <header>
      <h1>The Adventurer's Spellbook</h1>
      <spell-filter></spell-filter>
      <spell-list :spells="spells">
      </spell-list>
    </header>
  </div>
</template>

<script>
import { eventBus } from "@/main.js"
import SpellList from "@/components/spellList";
import SpellFilter from "@/components/spellFilter";

export default {
  name:"app",
  components: {
    "spell-list": SpellList,
    "spell-filter": SpellFilter
  },
  data() {
    return {
      rawSpells:[],
      spells: [],
      filteredSpellsList: [],
      selectedSpell: null,
      filterValue: ""
    };
  },
  methods: {
    getRawSpells: function() {
      fetch("https://www.dnd5eapi.co/api/spells")
      .then(response => response.json())
      .then(spells => this.rawSpells = spells.results)
      .then (() => this.getDetailedSpells())
      .then (() => this.filteredSpells());
    },

    getDetailedSpells: function() {
      for (const spell of this.rawSpells) {
        fetch(`https://www.dnd5eapi.co${spell.url}`)
        .then(response => response.json())
        .then(data => this.spells.push(data))
      }
    },
    // filteredSpells: function() {
    //   for (const spell of this.spells) {
    //     this.filteredSpellsList = spell.classes.filter(index => index.name === this.filterValue)
    //   }
    // }
  },

  mounted() {
    this.getRawSpells()

    eventBus.$on("spell-selected", spell => (this.selectedSpell = spell));

    eventBus.$on("filter-value", filterValue => (this.filterValue = filterValue));
  }
}
</script>

<style>

</style>