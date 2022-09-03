<template>
  <main>
    <b-alert v-model="showAlert" variant="danger" dismissible>
      {{ textAlert }}
    </b-alert>

    <b-overlay :show="showLoader" rounded="sm">
      <div class="container">
        <div class="row" v-for="(coinRow, index) in coins" :key="index">
          <div class="card" v-for="coin in coinRow" :key="coin.id" @click="loadCurrency(coin.name)">
            <b-img :src="coin.icon" width="100" height="100"></b-img>
            <div class="currency">1 {{ coin.name }} = {{ coin.currency }}</div>
          </div>
        </div>
      </div>
    </b-overlay>
  </main>
</template>

<script>
export default {
  name: 'Main',

  data: () => ({
    showLoader: false,
    showAlert: false,
    textAlert: '',
    coins: [
      [
        { id: 1, name: 'BTC', icon: '/images/btc.png', currency: '?' },
        { id: 2, name: 'ETH', icon: '/images/eth.png', currency: '?' },
      ],
      [
        { id: 3, name: 'USDT', icon: '/images/usdt.png', currency: '?' },
        { id: 4, name: 'USDC', icon: '/images/usdc.png', currency: '?' },
      ],
    ],
  }),

  methods: {
    loadCurrency(currency) {
      const self = this;
      self.showLoader = true;
      setTimeout(() => {
        this.coins.forEach(function(coins) {
          coins.forEach(function(coin) {
            if (coin.name === currency) {
              self.getCurrencyRate(coin.name)
                .then(response => response.json())
                .then(data => {
                  if (data.data) {
                    const priceUsd = Number(data.data.priceUsd).toFixed(2);
                    coin.currency = priceUsd;
                  }
                })
                .catch(error => {
                  self.setError(error.message);
                })
                .finally(() => self.showLoader = false);
            } else {
              self.showLoader = false;
            }
          })
        });
      }, 2000);
    },
    setError(error) {
      this.textAlert = error;
      this.showAlert = true;
    },
    getCurrencyRate(currency) {
      const url = this.getUrlByCurrency(currency);
      return fetch(url)
    },
    getUrlByCurrency(currency) {
      const url ='https://api.coincap.io/v2/assets/';

      switch (currency) {
        case 'BTC': return url + 'bitcoin';
        case 'ETH': return url + 'ethereum';
        case 'USDT': return url + 'tether';
        case 'USDC': return url + 'usd-coin';
      }
    }
  },

  created() {
    const self = this;
    this.coins.forEach(function(coins) {
      coins.forEach(coin => {
        self.loadCurrency(coin.name);
      })
    })
  }
};
</script>

<style lang="scss">
main {
  flex: 1;
  display: flex;
  justify-content: center;
  align-items: center;
}

.row {
  justify-content: center;
}

@media (max-width: 767px) {
  .container {
    margin-top: 2em;
    margin-bottom: 2em;
  }

  .row {
    flex-direction: column;
    align-items: center;
  }

  .card {
    margin: 2em 0 !important;
  }
}

.alert {
  z-index: 100;
  position: fixed;
  top: 100px;

  .close {
    border: none;
    background-color: #f8d7da;
    color: #B0413E;
    font-size: 1.5em;
  }
}

.card {
  width: 170px;
  height: 170px;
  margin: 10px;
  padding-top: 20px;
  text-align: center;
  cursor: pointer;

  &:hover {
    box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.1);
    opacity: 0.8;
  }

  img {
    margin: 0 auto;
  }

  .currency {
    margin-top: 12px;
  }
}
</style>
