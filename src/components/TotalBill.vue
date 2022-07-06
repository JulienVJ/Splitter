<template>
<div class="tips">
    <div class="tips-total">
        <div class="tips-total__amount">
            <p>Tips Amount<br><span>/ people</span></p>
            <p class="dollar">${{ tipsByPerson !== 0 ? tipsByPerson : "0" }}</p>    
        </div>
        <div class="tips-total__all">
            <p>Total<br><span>/ people</span></p>
            <p class="dollar">${{ total !== 0 ? total : "0" }}</p>
        </div>
        <div class="tips-total__reset">
            <button @click="resetAll">Reset</button>
        </div>
    </div>    
</div>
  
</template>

<script>
import bus from "@/services/bus";

export default {
    name: 'TotalBill',
    props: {
        tipsByPerson: Number,
        total: Number,
    },
    methods: {
        resetAll(){
           bus.emit("reset");
        }
    }
}

</script>

<style lang="scss">
.tips {
    @media (min-width: 900px) {
        height: 100%;
        }
}
.tips-total {
    background-color: $Very_dark;
    border-radius: 10px;
    padding: 25px;
    font-weight: 700;
    margin-top: 30px;
    @media (min-width: 900px) {
        height: 76%;
        margin: 30px;
        }

    &__amount {
        display: flex;
        align-content: center;
        justify-content: space-between;
        margin-bottom: 20px;
        p {
            color: $White;
        }
        span {
            color: $Grayish;
        }
        .dollar {
            color: $Primary_cyan;
            font-size: 24px;
        }
    }
    &__all {
        display: flex;
        align-content: center;
        justify-content: space-between;
        p {
            color: $White;
            margin-bottom: 30px;
        }
        span {
            color: $Grayish;
        }
        .dollar {
            color: $Primary_cyan;
            font-size: 24px;
        }
    }
    &__reset {
        display: flex;
        justify-content: center;
        align-items: center;
        
        button {
            background-color: $Primary_cyan;
            color: $Very_dark;
            font-weight: 700;
            transition: .5s;
            padding: 20px;
            border: none;
            border-radius: 5px;
            width: 100%;
        }
    }
}
</style>