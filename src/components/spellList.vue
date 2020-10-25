<template>
    <div>
        <span class="spell-list" id="list-titles">
            <h2>Spell Name</h2>
            <h2>Level</h2>
            <h2>Magic School</h2>
            <h2>Casting Time</h2>
        </span>
        <div class="spell-list" v-if="filteredSpells.length">    
            <spell-list-item v-for="(spell) in this.filteredSpells" :spell="spell" :key="spell.index"></spell-list-item>
        </div>
        <div class="spell-list" v-if="!filteredSpells.length">    
            <spell-list-item v-for="(spell) in this.spells" :spell="spell" :key="spell.index"></spell-list-item>
        </div>
    </div>
</template>

<script>
import SpellListItem from "@/components/spellListItem";
export default {
    name: "spell-list",
    props: ["spells", "filteredSpells"],
    components: {
        "spell-list-item": SpellListItem
    },
}
</script>

<style>
.spell-list {
    max-height: 60vh;
    overflow-y: scroll;
}
#list-titles {
    display:grid;
    grid-template-columns: 25% 25% 25% 25%;
    border: 2px solid black;
    padding: 5px;
    background-color: rgba(193, 224, 175, 0.897);
}
</style>