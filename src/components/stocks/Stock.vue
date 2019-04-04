<template>
    <div class="col-sm-6 col-md-4">
        <div class="panel panel-success">
            <div class="panel-heading">
                <div class="panel-title">{{ stock.name }}
                    <small>(Price: {{ stock.price }} )</small>
                </div>
                <div class="panel-body">
                    <div class="pull-left">
                        <input type="number" class="form-control" placeholder="Quantity" width="30px" v-model="quantity" :class="{danger: insufficientFunds}">
                    </div>
                    <div class="pull-right">
                        <button class="btn btn-success" @click="buyStock" :disabled = "insufficientFunds || quantity <= 0 || !(Number.isInteger(Number(quantity)))"> {{ insufficientFunds ? 'insufficient Funds' : 'Buy' }}</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<style  scoped>
.danger{
        border: 1px solid red;
        width: 140px
    }
</style>
    


<script>

    export default {
        props: ['stock'],
        data(){
            return {
                quantity: 0
            }
        },
        computed: {
            insufficientFunds(){
                return this.quantity * this.stock.price > this.funds; 
            },
            funds(){
                return this.$store.getters.funds
            }
        },
        methods: {
            buyStock(){
                const order = {
                    stockId: this.stock.id,
                    stockPrice: this.stock.price,
                    quantity: this.quantity
                };
                console.log(order)
                this.$store.dispatch('buyStock', order)
                this.quantity = 0;
                
            }
        }
    }
</script>

<style>

</style>
