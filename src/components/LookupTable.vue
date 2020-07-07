<template>
        <table class="lookup-table" border="0">
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
                    <td>{{ exchangeLookup(row.exchange) }}</td>
                    <td>{{ row.currency }}/{{ row.priceCurrency }}</td>
                    <td>{{ row.price }}</td>
                </tr>
            </tbody>
        </table>
</template>

<script>
    export default {
        name: "LookupTable",
        props: ['response'],
        methods: {
            exchangeLookup(id) {
                let exchange = '';
                switch (id) {
                    case 'bitfinex':
                        exchange = 'Bitfinex';
                        break;
                    case 'coinbasepro':
                        exchange = 'Coinbase PRO';
                        break;
                    case 'kraken':
                        exchange = 'Kraken';
                        break;
                }
                return exchange;
            }
        },
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
        margin: 1em auto;
    }

    table {
        font-family: "Trebuchet MS", Arial, Helvetica, sans-serif;
        width: 100%;
        max-width: 800px;
        border-collapse: collapse;
        border-radius: 16px;
        overflow: hidden;
        box-shadow: 0 6px 20px 5px rgba(0,0,0,.05);
    }

    table td, table th {
        text-align: center;
        padding: 16px;
        width: 20%;
    }

    table tr {background-color: #ffffff;}

    table tr:nth-child(even){background-color: #efefef;}

    table tr:hover {background-color: #dddddd;}

    table th {
        padding-top: 12px;
        padding-bottom: 12px;
        background-color: dodgerblue;
        color: white;
    }
</style>