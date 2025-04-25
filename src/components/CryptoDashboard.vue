<template>
    <div class="crypto-dashboard">
      <h1>Crypto Tracker</h1>
  
      <input
        v-model="searchQuery"
        type="text"
        placeholder="Search coin..."
        class="search-box"
      />
  
      <div v-if="filteredCoins.length" class="coin-list">
        <div v-for="coin in filteredCoins" :key="coin.id" class="coin-card">
            <div class="coin-card">
  <img :src="coin.image" :alt="coin.name" style="margin-right: 10px;" width="30" />
  <div>
    <strong>{{ coin.name }}</strong> ({{ coin.symbol.toUpperCase() }})<br />
    Price: ${{ coin.current_price.toLocaleString() }}<br />
    Market Cap: ${{ coin.market_cap.toLocaleString() }}<br />
    24h Change: 
    <span :style="{ color: coin.price_change_percentage_24h >= 0 ? 'green' : 'red' }">
      {{ coin.price_change_percentage_24h.toFixed(2) }}%
    </span>
  </div>
</div>

        </div>
      </div>
      <div v-else>No coins found.</div>
    </div>
  </template>
  
  <script>
  import axios from 'axios';

  export default {
    components: {
        
    },
    name: 'CryptoDashboard',
    data() {
      return {
        coins: [],
        searchQuery: ''
      };
    },
    computed: {
      filteredCoins() {
        return this.coins.filter((coin) =>
          coin.name.toLowerCase().includes(this.searchQuery.toLowerCase())
        );
      }
    },
    mounted() {
      this.fetchData();
    },
    methods: {
      fetchData() {
        axios
          .get('https://api.coingecko.com/api/v3/coins/markets', {
            params: {
              vs_currency: 'usd',
              order: 'market_cap_desc',
              per_page: 100,
              page: 1,
              sparkline: true
            }
          })
          .then((response) => {
            this.coins = response.data;
          })
          .catch((error) => {
            console.error('Error fetching crypto data:', error);
          });
      }
    }
  };
  </script>
  
  <style scoped>
  
  .crypto-dashboard {
    max-width: 900px;
    margin: auto;
    padding: 20px;
    font-family: 'Segoe UI', sans-serif;
  }
  
  .search-box {
    width: 100%;
    padding: 10px;
    margin-bottom: 20px;
  }
  
  .coin-list {
    display: flex;
    flex-wrap: wrap;
    gap: 15px;
  }
  
  .coin-card {
    display: flex;
    align-items: center;
    border: 1px solid #ddd;
    padding: 10px;
    border-radius: 10px;
    width: 100%;
    max-width: 400px;
  }
  </style>
  