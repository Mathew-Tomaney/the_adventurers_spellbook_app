<template>
  <section v-if="selectedSpell" id="spell-box">
      <h2>{{selectedSpell.name}}</h2>
      <p>{{selectedSpell.desc[0]}}</p>
      <p v-if="selectedSpell.higher_level">{{selectedSpell.higher_level[0]}}</p>
      <p v-if="selectedSpell.range">Range: {{selectedSpell.range}}</p>
      <p>Components: {{selectedSpell.components[0]}}</p>
      <p v-if="selectedSpell.material">Materials required: {{selectedSpell.material}}</p>
      <p>Duration: {{selectedSpell.duration}}</p>
      <p v-if="selectedSpell.concentration">Requires concentration.</p>
      <p v-if="selectedSpell.ritual">Can be cast as a ritual</p>
  </section>
</template>

<script>
export default {
    name: "spell-detail",
    props: ["selectedSpell"]

}
</script>

<style>
section {
    border: 20px groove forestgreen;
    margin: 0px 20px 0 20px;
    padding: 20px;
}
</style>