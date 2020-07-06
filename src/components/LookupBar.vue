<template>
    <div class="lookup-bar">
        <select id="currency" class="lookup-bar_option">
            <option value="BTC">Bitcoin</option>
        </select>
        <select id="price-currency" class="lookup-bar_option">
            <option value="EUR">€ Euro</option>
            <option value="USD">$ US Dollar</option>
        </select>
        <input id="start-date" type="date">
        <input id="end-date" type="date">
        <button class="lookup-bar_confirm">GO</button>
    </div>
</template>

<script>
    export default {
        name: "LookupBar"
    }
</script>

<style scoped>
    .lookup-bar {
        display: block;
    }

    .lookup-bar_option {

    }
</style>