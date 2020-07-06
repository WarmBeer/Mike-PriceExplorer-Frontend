<template>
    <div class="lookup-table">
        <table>
            <thead>
                <tr>
                    <th>#</th>
                    <th>Date</th>
                    <th>Exchange</th>
                    <th>Pair</th>
                    <th>Price</th>
                </tr>
            </thead>

            <tbody>
                <tr v-for="(row, index) in this.response.data" :key="index">
                    <td>{{ index + 1 }}</td>
                    <td>{{ new Date(row.date).toDateString() }}</td>
                    <td>{{ row.exchange }}</td>
                    <td>{{ row.currency }}/{{ row.priceCurrency }}</td>
                    <td>{{ row.price }}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
    export default {
        name: "LookupTable",
        props: ['response'],
        computed: {
            prices() {
                let prices = []
                return prices;
            }
        }
    }
</script>

<style scoped>
    .lookup-table {
        margin: 1em 2em;
        display: grid;
    }
</style>