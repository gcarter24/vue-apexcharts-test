<template>
  <div class="chart-wrapper">
    <div v-for="stock in series" v-bind:key="stock.id">
      <apexchart width="800" type="bar" :options="options" :series="series"></apexchart>
      {{ stock.data[0].close }}
      <!-- Stock Close: {{ stock.close }} -->
    </div>
    <div><button @click="updateChart">Update!</button></div>
  </div>
  <!-- <div id="main">
      <div class="field">
        <label for="title">SearchStocks</label>
        <input type="text" v-model="symbol" placeholder="Search" />
        <a v-on:click="searchStocks()" class="button primary">Search Stock History</a>
      </div> -->
</template>
<script>
import axios from "axios";
import VueApexCharts from "vue-apexcharts";
import Vue from "vue";
Vue.use(VueApexCharts);
Vue.component("apexchart", VueApexCharts);
export default {
  name: "HelloWorld",
  data: function() {
    return {
      stocks: [],
      symbol: "",
      close: 0,
      date: "",
      options: {
        chart: {
          id: "vuechart-example",
        },
        xaxis: {
          categories: ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"],
        },
        title: {
          text: "Monthly Stock Pricing",
          align: "center",
          style: {
            fontSize: "20px",
          },
        },
        colors: ["#00897b"],
      },
      series: [
        {
          name: "series-1",
          data: [],
        },
      ],
    };
  },
  created() {
    // console.log(this.$route.params.id);
    // axios.get(`/api/stocks/${this.$route.params.id}`).then(response => {
    //   console.log(response.data);
    //   this.stock = response.data;
    // });
    this.searchStocks();
    this.updateChart();
  },
  methods: {
    searchStocks() {
      console.log("stock");
      axios
        .get(`/api/stocks/stocks?search=ibm`)
        .then(response => {
          // this.stock = [
          //   {
          //     data: response.data.close,
          //   },
          // ];
          console.log(response.data);
          this.stocks = response.data;
        })
        .catch(error => {
          console.error(error);
        });
    },
    updateChart() {
      axios
        .get(`/api/stocks/stocks?search=ibm`)
        .then(response => {
          (this.series = [
            {
              data: response.data,
            },
          ]),
            console.log(response.data);
        })
        .catch(error => {
          console.error(error);
        });
    },
  },
};
</script>
<style scoped>
div.chart-wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>

<!-- <template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>
      For a guide and recipes on how to configure / customize this project,
      <br />
      check out the
      <a href="https://cli.vuejs.org" target="_blank" rel="noopener">vue-cli documentation</a>
      .
    </p>
    <h3>Installed CLI Plugins</h3>
    <ul>
      <li>
        <a
          href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-babel"
          target="_blank"
          rel="noopener"
        >
          babel
        </a>
      </li>
      <li>
        <a
          href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-router"
          target="_blank"
          rel="noopener"
        >
          router
        </a>
      </li>
      <li>
        <a
          href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-eslint"
          target="_blank"
          rel="noopener"
        >
          eslint
        </a>
      </li>
    </ul>
    <h3>Essential Links</h3>
    <ul>
      <li><a href="https://vuejs.org" target="_blank" rel="noopener">Core Docs</a></li>
      <li><a href="https://forum.vuejs.org" target="_blank" rel="noopener">Forum</a></li>
      <li><a href="https://chat.vuejs.org" target="_blank" rel="noopener">Community Chat</a></li>
      <li><a href="https://twitter.com/vuejs" target="_blank" rel="noopener">Twitter</a></li>
      <li><a href="https://news.vuejs.org" target="_blank" rel="noopener">News</a></li>
    </ul>
    <h3>Ecosystem</h3>
    <ul>
      <li><a href="https://router.vuejs.org" target="_blank" rel="noopener">vue-router</a></li>
      <li><a href="https://vuex.vuejs.org" target="_blank" rel="noopener">vuex</a></li>
      <li>
        <a href="https://github.com/vuejs/vue-devtools#vue-devtools" target="_blank" rel="noopener">vue-devtools</a>
      </li>
      <li><a href="https://vue-loader.vuejs.org" target="_blank" rel="noopener">vue-loader</a></li>
      <li><a href="https://github.com/vuejs/awesome-vue" target="_blank" rel="noopener">awesome-vue</a></li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
};
</script>

<style scoped>
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
  color: #1275d1;
}
</style> -->
