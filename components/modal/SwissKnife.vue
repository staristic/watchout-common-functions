<template>
<div class="modal swiss-knife">
  <div class="name">{{ activePersona ? (activePersona.name ? activePersona.name : '你的顯示名稱') : '沒有人' }}</div>
  <div class="actions">
    <a class="action" :href="activePersona ? getParkPersonaProfileURL(activePersona.id) : '#'">個人檔案</a>
    <a class="action" :href="getParkSettingsURL()">變更設定</a>
    <a class="action" @click="logoutAndRemoveModal">登出</a>
  </div>
</div>
</template>

<script>
import { knowsAuth, knowsWatchout, knowsWindowManagement } from '../../interfaces'
export default {
  mixins: [knowsAuth, knowsWatchout, knowsWindowManagement],
  methods: {
    logoutAndRemoveModal() {
      this.logout()
      this.removeModal('swiss-knife')
    }
  }
}
</script>

<style lang="scss">
@import '~watchout-common-assets/styles/resources';

.modal.swiss-knife {
  width: 18rem;
  background-color: $color-park-light;
  @include shadow;
  > .name {
    padding: 1rem;
    font-weight: bold;
    background-color: $color-park-light;
  }
  > .actions {
    > .action {
      display: block;
      padding: 1rem;
    }
  }
}
</style>
