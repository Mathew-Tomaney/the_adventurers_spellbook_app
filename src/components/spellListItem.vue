<template>
    <div v-on:click="selectSpell" class="spell-list-item">
        <span class="list-line">
            <h4 class="list-item-name">{{spell.name}}</h4>
            <p class="list-item">{{spell.level}}</p>
            <p class="list-item">{{spell.school.name}}</p>
            <p class="list-item">{{spell.casting_time}}</p>
        </span>
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
.list-line{
    display: grid;
    align-items: center;
    grid-template-columns: 25% 25% 25% 25%;
    border: 1px solid grey;
    
}

#list-item-name{
    padding: 0 10px 0 0;
}

</style>