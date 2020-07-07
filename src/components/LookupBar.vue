<template>
    <div class="lookup-bar">
        <select v-model="currency" id="currency" class="lookup-bar_option" @change="$emit('currency', currency)">
            <option value="BTC">Bitcoin</option>
        </select>
        <select v-model="priceCurrency" id="price-currency" class="lookup-bar_option" @change="$emit('priceCurrency', priceCurrency)">
            <option value="EUR">€ Euro</option>
            <option value="USD">$ US Dollar</option>
        </select>
        <input v-model="startDate" id="start-date" type="date" class="lookup-bar_option" @change="$emit('startDate', startDate)">
        <button class="lookup-bar_confirm" @click="$emit('clicked')">GO</button>
    </div>
</template>

<script>
    export default {
        name: "LookupBar",
        data: () => ({
            currency: 'BTC',
            priceCurrency: 'EUR',
            startDate: ''
        }),
        mounted() {
            let now = new Date();
            let day = ("0" + now.getDate()).slice(-2);
            let month = ("0" + (now.getMonth() + 1)).slice(-2);
            let today = now.getFullYear()+"-"+(month)+"-"+(day) ;
            this.startDate = today;
        }
    }
</script>

<style scoped>
    .lookup-bar {
        margin: auto;
        display: grid;
        grid-template-columns: 2fr 2fr 2fr 1fr;
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