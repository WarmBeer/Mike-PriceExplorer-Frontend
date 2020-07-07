<template>
    <div class="lookup-bar">
        <select v-model="exchange" id="exchange" class="lookup-bar_option" @change="$emit('exchange', exchange)">
            <option value="bitfinex">Bitfinex</option>
            <option value="kraken">Kraken</option>
            <option value="coinbasepro">Coinbase PRO</option>
        </select>
        <button class="lookup-bar_confirm" @click="$emit('clicked')">EXPORT all data to Excel</button>
    </div>
</template>

<script>
    export default {
        name: "ExportExcel",
        data: () => ({
            exchange: 'bitfinex'
        })
    }
</script>

<style scoped>
    .lookup-bar {
        margin: 1em auto;
        display: grid;
        grid-template-columns: 2fr 1fr;
        width: auto;
        max-width: 800px;
        border-radius: 16px;
        overflow: hidden;
    }

    .lookup-bar_option, .lookup-bar_confirm {
        border: none;
        background-color: #eeeeee;
        border-radius: 0;
        padding: 16px;
        outline: none;
        font-weight: bold;
    }

    .lookup-bar_confirm {
        background-color: #1e90ff;
        color: #effeee;
    }

    .lookup-bar_confirm:hover {
        background-color: #1eb0ff;
        cursor: pointer;
    }
</style>