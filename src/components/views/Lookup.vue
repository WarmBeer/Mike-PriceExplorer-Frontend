<template>
  <section class="body">
    <h1>{{ 'Lookup Crypto price history' }}</h1>
    <lookup-bar
            @currency="currency = $event"
            @priceCurrency="priceCurrency = $event"
            @startDate="startDate = new Date($event).getTime()"
            @clicked="getData()"
    ></lookup-bar>
    <h2 v-if="response.data.length < 1">This date is unavailable.</h2>
    <lookup-table v-else :response="response"></lookup-table>
    <export-excel
            @exchange="exchange = $event"
            @clicked="download()"
    ></export-excel>
  </section>
</template>

<script>
import LookupBar from "../LookupBar";
import LookupTable from "../LookupTable";
import ExportExcel from "@/components/ExportExcel";
export default {
  name: 'Lookup',
  components: {ExportExcel, LookupTable, LookupBar},
  props: {
    msg: String
  },
  data: () => ({
    response: {
      data: []
    },
    currency: 'BTC',
    priceCurrency: 'EUR',
    startDate: '',
    exchange: 'bitfinex'
  }),
  methods: {
    getData() {
      fetch(`http://localhost:3010/price/${this.currency}?priceCurrency=${this.priceCurrency}&startDate=${this.startDate}`)
        .then((res) => res.json())
        .then((res) => {
          this.response = res;
        });
    },
    download() {
      const mimeType = 'text/csv;encoding:utf-8'
      const fileName = `${this.exchange}-${Date.now()}.csv`;
      let data = '';
      fetch(`http://localhost:3010/price/${this.currency}?priceCurrency=${this.priceCurrency}&exchange=${this.exchange}&startDate=0&endDate=${Date.now()}`)
              .then((res) => res.json())
              .then((res) => {
                data = res.data;
                let csvContent = '';
                data.forEach((row, index) => {
                  let date = new Date(row.date);
                  let day = ("0" + date.getDate()).slice(-2);
                  let month = ("0" + (date.getMonth() + 1)).slice(-2);
                  date = date.getFullYear()+"-"+(month)+"-"+(day) ;
                  let dataString = `${date},${row.exchange},${row.currency}/${row.priceCurrency},${row.price}`;
                  csvContent += index < data.length ? dataString + '\n' : dataString;
                });
                let a = document.createElement('a');

                if (navigator.msSaveBlob) { // IE10
                  navigator.msSaveBlob(new Blob([csvContent], {
                    type: mimeType
                  }), fileName);
                } else if (URL && 'download' in a) { //html5 A[download]
                  a.href = URL.createObjectURL(new Blob([csvContent], {
                    type: mimeType
                  }));
                  a.setAttribute('download', fileName);
                  document.body.appendChild(a);
                  a.click();
                  document.body.removeChild(a);
                } else {
                  location.href = 'data:application/octet-stream,' + encodeURIComponent(csvContent); // only this mime type is supported
                }
              });
    }
  },
  mounted() {
    let thisDate = new Date();
    this.startDate = new Date(Date.UTC(thisDate.getFullYear(), thisDate.getMonth(), thisDate.getDate())).getTime();
    this.getData();
  }
}
</script>

<style scoped>
  section.body {
    margin: 0 2em;
  }

  h3 {
    margin: 40px 0 0;
  }
  ul {
    list-style-type: none;
    padding: 0;
  }
  li {
    display: inline-block;
    margin: 0 10px;
  }
  a {
    color: #42b983;
  }
</style>
