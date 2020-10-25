<template>
  <section v-if="selectedSpell" id="spell-box">
      <h2>{{selectedSpell.name}}</h2>
      <p>{{selectedSpell.desc[0]}}</p>
      <p v-if="selectedSpell.higher_level">{{selectedSpell.higher_level[0]}}</p>
      <p>Range: {{selectedSpell.range}}</p>
      <p>Components: {{selectedSpell.components[0]}}</p>
      <p>Ritual? {{selectedSpell.ritual}}</p>
      <p>Materials required: {{selectedSpell.material}}</p>
      <p>Duration: {{selectedSpell.duration}}</p>
      <p>Contentration? {{selectedSpell.concentration}}</p>
  </section>
</template>

<script>
export default {
    name: "spell-detail",
    props: ["selectedSpell"]

}
</script>

<style>

</style>