<template>
  <div id="filter">
        <div class="label-and-radio1">
            <label for="All">All:</label>
            <input v-on:change="filterSpells()" type="radio" id="All" name="filter-inputs" value="All"      v-model="filterValue">
        </div>
        <div class="label-and-radio2">
            <label for="Bard">Bard:</label>
            <input v-on:change="filterSpells()" type="radio" id="Bard" name="filter-inputs" value="Bard"    v-model="filterValue">
        </div>
        <div class="label-and-radio1">
            <label for="Cleric">Cleric:</label>
            <input v-on:change="filterSpells()" type="radio" id="Cleric" name="filter-inputs" value="Cleric"    v-model="filterValue">
        </div>
        <div class="label-and-radio2">
            <label for="Druid">Druid:</label>
            <input v-on:change="filterSpells()" type="radio" id="Druid" name="filter-inputs" value="Druid"      v-model="filterValue">
        </div>
        <div class="label-and-radio1">
            <label for="Paladin">Paladin:</label>
            <input v-on:change="filterSpells()" type="radio" id="Paladin" name="filter-inputs"  value="Paladin"    v-model="filterValue">
        </div>
        <div class="label-and-radio2">
            <label for="Ranger">Ranger:</label>
            <input v-on:change="filterSpells()" type="radio" id="Ranger" name="filter-inputs" value="Ranger"    v-model="filterValue">
        </div>
        <div class="label-and-radio1">
            <label for="Sorcerer">Sorcerer:</label>
            <input v-on:change="filterSpells()" type="radio" id="Sorcerer" name="filter-inputs"     value="Sorcerer"  v-model="filterValue">
        </div>
        <div class="label-and-radio2">
            <label for="Warlock">Warlock:</label>
            <input v-on:change="filterSpells()" type="radio" id="Warlock" name="filter-inputs"  value="Warlock"    v-model="filterValue">
        </div>
        <div class="label-and-radio1">
            <label for="Wizard">Wizard:</label>
            <input v-on:change="filterSpells()" type="radio" id="Wizard" name="filter-inputs" value="Wizard"    v-model="filterValue">
        </div>
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
            eventBus.$emit("filter-value", this.filterValue)
        },
    },
}
</script>

<style lang="css" scoped>
#filter {
    display:flex;
}
.label-and-radio1 {
    background-color: rgba(72, 133, 64, 0.657);
    padding: 10px;
}
.label-and-radio2 {
    background-color: rgba(167, 206, 79, 0.657);
    padding: 10px;
}
input {
    cursor: pointer;
}
</style>