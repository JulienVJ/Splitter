<template>
<div class="headerLogo">
  <img class="logoIm" src="./assets/images/logo.svg" alt="logo App">
</div>
<div class="mainContent">
  <div class="bill-total-section">
      <BillCard
        @percentage-tips="(p) => tipsByPerson = p" 
        @total="(t) => total = t"
      />
      <TotalBill
        :tipsByPerson="tipsByPerson"
        :total="total"
       />
  </div>

</div>
</template>

<script>
import BillCard from './components/BillCard.vue'
import TotalBill from './components/TotalBill.vue'

export default {
  name: 'App',
  components: {
    BillCard,
    TotalBill,
  },
  data() {
        return {
            tipsByPerson: 0,
            total: 0,

        }
    },
}
</script>

<style lang="scss">
  @media (min-width: 900px) {
    body {
      background-color: $Light_grayish;
      display: flex;
      justify-content: center;
      align-content: center;
    }
    .bill-total-section {
      background-color: $White;
      padding: 10px;
      border-radius: 10px;
      border: none;
      @media (min-width: 900px) {
      display: grid;
      grid-template-columns: 1fr 1fr;
    }
    }
  }

  .mainContent {
    padding: 30px;
    @media (min-width: 900px) {
      padding: 30px;
      max-width: 1000px;
    }
}

  .headerLogo {
    background-color: $Light_grayish;
    height: 150px;
    display: flex;
    justify-content: center;
    align-items: center;

  }
</style>
