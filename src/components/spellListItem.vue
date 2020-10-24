<template>
    <div class="spell">
        <span>{{spell.name}}  Level: {{spell.level}}  School: {{spell.school.index}}  Casting Time: {{spell.casting_time}}</span>
    </div>
  
</template>

<script>
export default {
    name: "spell-list-item",
    props: ["spell"]

}
</script>

<style>

</style>