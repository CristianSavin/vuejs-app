<template>
    <div class="row">
        <app-stock v-for="(stock, index) in stocks" :key="index * 2" :stock="stock"></app-stock>
    </div>
</template>

<script>
    import {mapGetters} from 'vuex';
    import Stock from './Stock.vue';
    export default {
        computed: {
            ...mapGetters({
                stocks: 'stockPortfolio'
            })
        },
        components: {
            appStock: Stock
        }
    }
</script>

<style>
    .row{
        padding: 20px 0;
    }
</style>
