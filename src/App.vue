<template>
  <div id=app>
    <header>
      <h1>The Adventurer's Spellbook</h1>
    </header>
    <main>
      <spell-filter></spell-filter>
      <spell-list :spells="spells" :filteredSpells="filteredSpellsList"></spell-list>
    </main>
    <aside>
      <spell-detail :selectedSpell="selectedSpell"></spell-detail>
    </aside>
    <footer>
      <h4>Thanks for checking it out!</h4>
    </footer>
  </div>
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

/* #app {
  display: grid;
  grid-template-columns: 50% 50%;
  grid-template-rows: 100px auto 100px;
  max-height: 100vh;
  grid-template-areas: 
    "header header"
    "list boxes"
    "footer footer";
}

#app > header {
  grid-area: header;
}

main {
  grid-area: list;
}

aside {
  grid-area: boxes;
}

footer {
  grid-area: footer;
} */
</style>