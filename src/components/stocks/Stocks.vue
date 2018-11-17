<template>
    <div class='stock-wrap row'>
        <app-stock 
            v-for="(stock, index) in stocks" :key="index + stock.name"
            :stock="stock"></app-stock>
    </div>
</template>

<script>
    import Stock from './Stock';
    export default {
        data() {
            return {
                
            }
        },
        components: {
            appStock: Stock
        },
        computed: {
            stocks() {
                return this.$store.getters.stocks
            }
        }  
    }
</script>

<style>
    .stock-wrap{
        padding: 20px 0;
    }
</style>

