<template>
  <form class="popup" @submit.prevent>
    <div class="popup-inner">
      <div class="popup__header">
        <h2 class="popup__header-title">Налоговый вычет</h2>
        <p class="popup__header-text">Используйте налоговый вычет чтобы погасить ипотеку досрочно.
          Размер налогового вычета составляет не более 13% от своего официального годового дохода.</p>
        <button @click="$emit('click')" class="popup__header-close"></button>
      </div>
      <div class="popup__input">
        <label for="salary">Ваша зарплата в месяц</label>
        <input id="salary" type="number" v-model="number" placeholder="Введите данные">
      </div>
      <button @click="checkNalog(nalog)" type="button" class="popup__button-salary">Расчитать</button>
      <List :items="numbers" v-if="isShowList"/>
      <div class="popup__change">
        <h3 class="popup__change-title">Что уменьшаем?</h3>
        <button v-for="(item,idx) in buttonsChange"
        :key="idx" class="popup__change-btn"
        type="button"
        :class="{'active':item.active}"
        @click="isActiveChangeButton(buttonsChange)"
        >{{item.text}}</button>
      </div>
    </div>
    <div class="popup__footer">
      <button type="submit" class="popup__button-add" @click.prevent>Добавить</button>
    </div>
  </form>
</template>

<script>
import List from '../list/index.vue'
export default {
  name: 'Popup',
  components: {
    List
  },
  data: ()=>({
    number: null,
    nalogNumber: null,
    maxNalog: 260000,
    numbers: [],
    num: null,
    isShowList: false,
    numZel: null,
    buttonsChange: [{
      text: 'Платеж',
      active: true
    },{
      text: 'Срок',
      active: false
    }]
  }),
  computed: {
    nalog() {
     return this.number * 12 * 0.13
    }
  },
  methods: {
    isActiveChangeButton(arr) {
      for(let i = 0; i <= arr.length;i++) {
        arr.forEach(el=> {
          el.active = !el.active
        })
      }
    },
    checkNalog() {
    this.numZel = Math.floor(this.maxNalog/this.nalog)
    this.num = this.maxNalog % this.nalog
    this.checkNalogZel()
    },
    checkNalogZel() {
      this.isShowList = !this.isShowList
      let arr = [];
      for (let i = 0; i < this.numZel; i++) {
          arr.push(this.nalog);
      }
      arr.push(this.num);
      this.numbers = arr;
    }
  }
}
</script>

<style lang="scss" src="./index.scss">

</style>