<template>
    <div class="spell-list" v-if="spells.length">    
        <li v-for="(spell) in this.spells" :key="spell.index"> {{spell.name}}  Level: {{spell.level}}  School: {{spell.school.index}}  Casting Time: {{spell.casting_time}}</li>
    </div>
</template>

<script>

export default {
    name: "spell-list",
    props: ["spells"]
    
}
</script>

<style>

</style>