<template>
  <main>
    <header>
      <h1>The Adventurer's Spellbook</h1>
    </header>
    <ul>
      <spell-filter></spell-filter>
      <spell-list :spells="spells" :filteredSpells="filteredSpellsList"></spell-list>
    </ul>
    <aside>
      <spell-detail :selectedSpell="selectedSpell"></spell-detail>
    </aside>
    <footer>
      <h4>Thanks for checking it out!</h4>
    </footer>
  </main>
</template>

<script>
import { eventBus } from "@/main.js"
import SpellList from "@/components/spellList";
import SpellFilter from "@/components/spellFilter";
import SpellDetail from "@/components/spellDetail";


export default {
  name:"app",
  components: {
    "spell-list": SpellList,
    "spell-filter": SpellFilter,
    "spell-detail": SpellDetail
  },
  data() {
    return {
      rawSpells:[],
      spells: [],
      filteredSpellsList: [],
      selectedSpell: null,
      filterValue: "All"
    };
  },
  
  methods: {
    getRawSpells: function() {
      fetch("https://www.dnd5eapi.co/api/spells")
      .then(response => response.json())
      .then(spells => this.rawSpells = spells.results)
      .then (() => this.getDetailedSpells())
    },

    getDetailedSpells: function() {
      for (const spell of this.rawSpells) {
        fetch(`https://www.dnd5eapi.co${spell.url}`)
        .then(response => response.json())
        .then(data => this.spells.push(data))
      }
    },

    filteredSpells: function(filterValue) {
      let spell;
      let i;
      this.filteredSpellsList= []
      for (let spell of this.spells) {
        for (let i of spell.classes) {
          if (filterValue !== "All" && i.name === filterValue) {
            this.filteredSpellsList.push(spell)
          }
        }
      }
    }
  },

  mounted() {
    this.getRawSpells()
    
    eventBus.$on("spell-selected", spell => (this.selectedSpell = spell));

    eventBus.$on("filter-value", filterValue => (this.filteredSpells(filterValue)));
  }
}
</script>

<style lang="css" scoped>

body {
  margin:0;
  padding:0;
}

main {
  margin:0 0 0 0;
  padding:0 0 0 0;
  display: grid;
  grid-template-columns: 50% 50%;
  grid-template-rows: 100px auto 100px;
  max-height: 100vh;
  grid-template-areas: 
    'header header'
    'list boxes'
    'footer footer';
  background-color: rgba(48, 110, 48, 0.445);
}

header {
  grid-area: header;
  background: linear-gradient(rgb(29, 93, 29), green);
  color:gainsboro;
}
header > h1 {
  font-family: fantasy;
  font-size: 35pt;
  padding: 20px;
  margin:0;
}

ul {
  grid-area: list;
  margin:0;
  padding:0;
  background-color: white;
}

aside {
  grid-area: boxes;
}

footer {
  grid-area: footer;
  display: flex;
  justify-content: flex-end;
  background:linear-gradient(green, rgb(29, 93, 29));
  color:gainsboro;
  margin:0;
}

footer > h4 {
  padding: 20px;
  font-family: fantasy;
  font-size: 25pt;
  margin:5px;
}
</style>