<template>
  <form class="popup" @submit.prevent>
    <div class="popup__inner">
      <div class="popup__header">
        <h2 class="popup__header-title">Налоговый вычет</h2>
        <p class="popup__header-text">Используйте налоговый вычет чтобы погасить ипотеку досрочно.
          Размер налогового вычета составляет не более 13% от своего официального годового дохода.</p>
        <button @click="$emit('click')" class="popup__header-close"></button>
      </div>
      <div class="popup__input">
        <label for="salary">Ваша зарплата в месяц</label>
        <input id="salary" type="number" v-model="salary" placeholder="Введите данные">
      </div>
      <button @click="checkTax(a)" type="button" class="popup__button-salary">Расчитать</button>
      <List :items="taxNumber" v-if="isShowList"/>
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
    salary: null,
    taxNumber: null,
    maxTax: 260000,
    numbers: [],
    num: null,
    isShowList: false,
    numWole: null,
    buttonsChange: [{
      text: 'Платеж',
      active: true
    },{
      text: 'Срок',
      active: false
    }]
  }),
  computed: {
    paymentTax() {
     return this.salary * 12 * 0.13
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
    checkTax() {
    this.numWole= Math.floor(this.maxTax/this.paymentTax)
    this.num = this.maxTax % this.paymentTax
    this.checkQuantity()
    },
    checkQuantity() {
      this.isShowList = !this.isShowList
      let arr = [];
      for (let i = 0; i < this.numWole; i++) {
          arr.push(this.Tax);
      }
      arr.push(this.num);
      this.taxNumber = arr;
    }
  }
}
</script>

<style lang="scss" src="./index.scss">

</style>