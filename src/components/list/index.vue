<template>
  <div class="list">
    <h3 class="list__title">Итого можете внести в качестве досрочных:</h3>
    <ul>
      <li v-for="(item,idx) in items" :key="idx">
        <div class="list__item">
          <input class="list__item-checkbox" type="checkbox" :id="idx" :name="idx">
          <label :for="idx">{{item}} рублей</label>
          <span>в {{idx+1}}{{ending(idx+1)}} год</span>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'List',
  props: {
    items: {
      type: Array,
      default: ()=> []
    }
  },
  methods: {
    ending(num) {
      if (num === 2) {
        return '-ой'
      } else {
        return '-ый'
      }
    }
  }

}
</script>

<style lang="scss" src="./list.scss">
</style>