<template>
    <div class='col-sm-6 col-md-4'>
        <div class="card text-white bg-primary mb-3">
            <div class="card-header">
                <h3 class='panel-title'>
                    {{ stock.name }}
                    <small>(Price: {{ stock.price }})</small>
                </h3>
            </div>
            <div class="card-body">
                <div class="float-left">
                    <input 
                        type="number"
                        class="form-control"
                        placeholder="Quantity"
                        v-model.number="quantity"
                        v-bind:class="{danger: insufficientFunds}"
                        >
                </div>
                <div class="float-right">
                    <button 
                        class="btn btn-success float-right"
                        @click="buyStock"
                        v-bind:disabled="insufficientFunds || !Number.isInteger(quantity) || quantity <= 0">
                        {{ insufficientFunds ? 'Insufficient Funds' : 'Buy' }}</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        props: ['stock'],
        data() {
            return {
                quantity: 0
            }
        },
        computed: {
            funds() {
                return this.$store.getters.funds;
            },
            insufficientFunds() {
                return this.quantity * this.stock.price > this.funds;
            }
        },
        methods: {
            updateQuantity(event) {
                this.quantity = event.target.value;
            },
            buyStock() {
                const order = {
                    stockId: this.stock.id,
                    stockPrice: this.stock.price,
                    quantity: this.quantity
                };
                this.$store.dispatch('buyStock', order);
                this.quantity = 0;
            }
        }   
    }
</script>


<style>
    .card-body{
        padding: 1.15rem;
    }
    .float-left{
        width: 49%;
    }
    .float-right{
        width: 49%;
    }
    button.float-right{
        clear: both;
        width: auto;
    }
    .danger {
        border: 1px solid red !important;
    }
</style>

