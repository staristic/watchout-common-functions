<template>
<nav :class="navClasses">
  <div class="nav-item switcher" v-if="channel.switcher.show" :style="switcherStyles" @click="addModal('transporter')"></div>
  <nuxt-link class="nav-item logo-with-type" :to="{ name: 'index' }">
    <img :src="getProjectLogoWithType(channel.id)" :style="getProjectLogoWithTypeStyles(channel.id)"/>
  </nuxt-link>
  <div class="nav-item menu-container"></div>
  <div class="nav-item search-container"></div>
  <div class="nav-item avatar-container" @click="isCitizen ? addModal('swiss-knife') : addModal({ id: 'auth', joinOrLogin: 'join' })">
    <avatar :avatar="isCitizen ? activePersona.avatar : 'anon'"/>
  </div>
</nav>
</template>

<script>
// FIXME: perhaps better not use relative path
import { knowsAuth, knowsWatchout, knowsWindowManagement } from '../interfaces'
import Avatar from './Avatar'

export default {
  mixins: [knowsAuth, knowsWatchout, knowsWindowManagement],
  props: ['channel'],
  computed: {
    whichSide() {
      return this.channel.isDark ? 'dark' : 'light'
    },
    navClasses() {
      return [
        this.channel.classes.backgroundColor.opaque
      ]
    },
    switcherStyles() {
      return {
        backgroundImage: 'url(' + require('watchout-common-assets/images/nav-button/switcher/' + (this.channel.switcher.dark ? 'dark' : 'light') + (this.channel.switcher.iconOnly ? '-icon-only' : '') + '.png') + ')'
      }
    }
  },
  created () {
    this.checkAuth()
  },
  components: {
    Avatar
  }
}
</script>

<style lang="scss">
@import '~watchout-common-assets/styles/resources';
nav {
  position: relative;
  display: flex;
  flex-direction: row;
  width: 100%;
  height: 64px;
  margin: 0;
  padding: 0;

  > .nav-item {
    flex-grow: 0;
  }
  > .switcher {
    flex-basis: 52px;
    background-size: cover;
    background-position: center;
    cursor: pointer;
  }
  > .logo-with-type {
    display: block;
    width: 64px;
    overflow-x: hidden;
    @include bp-sm-up {
      width: auto;
    }
  }
  > .menu-container {
    flex-grow: 1;
  }
  > .avatar-container {
    display: flex;
    flex-basis: 60px;
    justify-content: center;
    align-items: center;
    cursor: pointer;
  }
}
</style>
