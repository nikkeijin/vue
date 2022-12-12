<template>
  
  <TheHeader></TheHeader>
  <TheHero></TheHero>
  <TheContent></TheContent>
  <TheTech></TheTech>
  <TheStep></TheStep>
  <TheGallery></TheGallery>
  <TheContact></TheContact>
  <TheFooter></TheFooter>

</template>

<script>
import TheHeader from './components/TheHeader.vue'
import TheHero from './components/TheHero.vue'
import TheContent from './components/TheContent.vue'
import TheTech from './components/TheTech.vue'
import TheStep from './components/TheStep.vue'
import TheGallery from './components/TheGallery.vue'
import TheContact from './components/TheContact.vue'
import TheFooter from './components/TheFooter.vue'

export default {
  name: 'App',
  components: {
    TheHeader,
    TheHero,
    TheContent,
    TheTech,
    TheStep,
    TheGallery,
    TheContact,
    TheFooter
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
