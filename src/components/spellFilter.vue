<template>
  <div id="filter">
      <input v-on:change="filterSpells()" type="radio" id="All" name="filter-inputs" value="All" v-model="filterValue">
      <input v-on:change="filterSpells()" type="radio" id="Bard" name="filter-inputs" value="Bard" v-model="filterValue">
      <input v-on:change="filterSpells()" type="radio" id="Cleric" name="filter-inputs" value="Cleric" v-model="filterValue">
      <input v-on:change="filterSpells()" type="radio" id="Druid" name="filter-inputs" value="Druid" v-model="filterValue">
      <input v-on:change="filterSpells()" type="radio" id="Paladin" name="filter-inputs" value="Paladin" v-model="filterValue">
      <input v-on:change="filterSpells()" type="radio" id="Ranger" name="filter-inputs" value="Ranger" v-model="filterValue">
      <input v-on:change="filterSpells()" type="radio" id="Sorcerer" name="filter-inputs" value="Sorcerer" v-model="filterValue">
      <input v-on:change="filterSpells()" type="radio" id="Warlock" name="filter-inputs" value="Warlock" v-model="filterValue">
      <input v-on:change="filterSpells()" type="radio" id="Wizard" name="filter-inputs" value="Wizard" v-model="filterValue">
  </div>
</template>

<script>
import { eventBus } from "@/main.js";
export default {
    name: "spell-filter",
    data(){
        return {
            filterValue: "All"
        }
    },
    methods: {
        filterSpells: function() {
            eventBus.$emit("filter-value", this.filterValue);
        }
    }
}
</script>

<style>

</style>