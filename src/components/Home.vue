<template>
    <div class="container">
        <h1> Trade or view your profile</h1>
        <h3>You may Save and Load your data</h3>
        <h4>Click on 'End Day' to begin a new day</h4>
        <hr>
        <p>Your Funds: {{ funds | currency}}</p>
        <router-view></router-view>
    </div>
</template>

<script>

    export default {
        computed: {
            funds() {
                return this.$store.getters.funds;
            }
        }
    }
</script>

<style>

</style>
