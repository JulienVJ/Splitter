<template>
<div class="main-content">
    <div class="bill-section">
        <label class="bill-section__label">Bill</label>
        <input v-model="checkedTips.bill" class="bill-section__input"  type="number" placeholder="0"
        min="1" max="99999999999">
    </div>
    <label class="select-tip__label">Select Tip %</label>
    <div class="select-tip">
        <button :class="{'select-tip__button--selected': tip === checkedTips.percentage}" @click="checkedTips.percentage = tip" v-for='tip in tips' :key="tip" class="select-tip__button">{{ tip }}%</button>
        <input v-model="checkedTips.percentage" class="select-tip__customButton" type="number" placeholder="Custom">
    </div>
    <div class="people-section">
        <label class="people-section__label">Number of People</label>
        <input v-model="checkedTips.people" class="people-section__input" type="number" placeholder="0">
    </div>
</div>
</template>

<script>
import bus from "@/services/bus";

export default {
    name: 'BillCard',
    data() {
        return {
            tips:[5, 10, 15, 25, 50],
            checkedTips: {
                bill: 0,
                percentage: 0,
                people: 0
            },
        }
    },
    computed: {
        calculTips() {
            const {bill, percentage, people} = this.checkedTips;
            const calc = bill/100 * percentage / people
            return isNaN(calc) ? 0 : calc;
        },

        total() {
            const {bill, people} = this.checkedTips;
            const calc = bill / people + this.calculTips;
            return isNaN(calc) ? 0 : calc;
        },
    },
    watch: {
        calculTips(n){
            this.$emit('percentageTips', n);
        },
        total(n){
            this.$emit('total', n);
        }
    },
    mounted() {
        bus.on("reset", () => {
            this.checkedTips.bill = 0;
            this.checkedTips.percentage = 0;
            this.checkedTips.people = 0;
        })
    }
}
</script>

<style lang="scss">
.main-content {
    display: flex;
    flex-direction: column;
    gap: 30px;
    @media (min-width: 900px) {
        padding: 30px;
      }
}
.bill-section {
    display: flex;
    justify-content: center;
    flex-direction: column;
    &__label {
        color: $Dark_grayish;
        font-weight: 700;
        font-size: 18px;
        margin-bottom: 10px;
    }
    &__input {
        text-align: right;
        border-radius: 5px;
        border: none;
        color: $Very_dark;
        font-size: 24px;
        font-weight: 700;
        background: no-repeat center left 15px,$Very_light_grayish;
        height: 100%;
        padding: 5px;
    }
    
}
.select-tip__label {
    color: $Dark_grayish;
    font-weight: 700;
    font-size: 18px;
    margin-top: 20px;
    left: 0;
}
.select-tip {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-template-rows: 1fr 1fr;
    gap: 15px;
    &__button {
        background-color: $Very_dark;
        color: $White;
        padding: 20px;
        border: none;
        border-radius: 5px;
        &--selected {
            background-color: $Primary_cyan;
        }
    }
    &__customButton {
    text-align: right;
    border-radius: 5px;
    border: none;
    color: #00494d;
    font-size: 22px;
    font-weight: 700;
    background: no-repeat center left 15px,$Very_light_grayish;
    width: 100%;
    }
}

.people-section {
    display: flex;
    justify-content: center;
    flex-direction: column;
    &__label {
        color: $Dark_grayish;
        font-weight: 700;
        font-size: 18px;
        margin-bottom: 10px;
    }
    &__input {
        text-align: right;
        border-radius: 5px;
        border: none;
        color: $Very_dark;
        font-size: 24px;
        font-weight: 700;
        background: no-repeat center left 15px, $Very_light_grayish;
        height: 100%;
        box-sizing: border-box;
        padding: 5px;
        }
    }

</style>