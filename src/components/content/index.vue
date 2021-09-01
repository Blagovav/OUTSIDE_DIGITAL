<template>
  <div class="content" :class="{'gray':isActive}">
    <button v-if="!isActive" type="button" class="content__button" @click="toogleActive">Налоговый вычет</button>
    <Popup v-if="isActive" @click="toogleActive"/>
  </div>
</template>

<script>
import Popup from '../popup/index.vue'
export default {
  name: 'Content',
  components: {
    Popup
  },
  data: ()=>({
    isActive: false
  }),
  methods: {
    toogleActive() {
      this.isActive = !this.isActive
    }
  }
}
</script>

<style lang="scss" src="./index.scss">

</style>