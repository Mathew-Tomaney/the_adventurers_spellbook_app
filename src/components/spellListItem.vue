<template>
    <div v-on:click="selectSpell" class="spell-list-item">
        <span>{{spell.name}}  Level: {{spell.level}}  School: {{spell.school.index}}  Casting Time: {{spell.casting_time}}</span>
    </div>
  
</template>

<script>
import {eventBus} from "@/main.js";
export default {
    name: "spell-list-item",
    props: ["spell"],

    methods: {
        selectSpell: function() {
            eventBus.$emit("spell-selected", this.spell);
        }
    }
}
</script>

<style>

</style>