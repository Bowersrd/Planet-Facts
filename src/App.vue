<template>
  <div class="fixed-bg"></div>
  <app-navbar :planets="planets" :activePlanet="activePlanet" @change-planet="changePlanet" @scroll-lock="scrollLock"></app-navbar>
  <main>
    <planet-info :planet="planets[activePlanet]" :currentView="views[currentView]" @change-tab="changeTab"></planet-info>
    <planet-stats :planet="planets[activePlanet]"></planet-stats>
  </main>
</template>

<script>
import AppNavbar from '@/components/AppNavbar';
import PlanetInfo from '@/components/PlanetInfo';
import PlanetStats from '@/components/PlanetStats';
import PlanetData from '../static/data.json';

export default {
  name: 'App',
  components: {
    'app-navbar': AppNavbar,
    'planet-info': PlanetInfo,
    'planet-stats': PlanetStats    
  },
  data() {
    return {
      planets: PlanetData,
      activePlanet: 0,
      currentView: 0,
      views: ['overview', 'structure', 'geology']
    }
  },
  methods: {
    changePlanet(index) {
      this.activePlanet = index;
      document.body.style.overflow = 'auto';
    },
    changeTab(index) {
      this.currentView = index;
    },
    scrollLock() {
      document.body.style.overflow == 'hidden' ? document.body.style.overflow = 'auto' : document.body.style.overflow = 'hidden';
    }
  }
}
</script>

<style lang="scss">
@import '@/assets/scss/style.scss';

body {
  background-color: var(--color-primary-500);
  background-size: cover;
  font-family: var(--ff-primary);
  color: var(--color-white);
}

.fixed-bg {
  // To support Safari since Safari does not support bg attachment at this time
  z-index: -1;
  position: fixed;
  top: 0;
  left: 0;
  height: 100%;
  width: 100%;
  background-image: url('@/assets/images/background-stars.svg');
  background-position: top left;
  background-size: cover;
}
</style>
