<template>
    <div class="spell-list" v-if="spells.length">    
        <spell-list-item v-for="(spell) in this.spells" :spell="spell" :key="spell.index"></spell-list-item>
    </div>
</template>

<script>
import SpellListItem from "@/components/spellListItem";
export default {
    name: "spell-list",
    props: ["spells"],
    components: {
        "spell-list-item": SpellListItem
    }
    
}
</script>

<style>

</style>