<template>
  <main>
    <div class="container">
      <div class="row" v-for="(coinRow, index) in coins" :key="index">
        <div class="card" v-for="coin in coinRow" :key="coin.name">
          <b-img :src="coin.icon" width="100" height="100"></b-img>
          <div class="currency">{{ coin.name }}</div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  name: 'Main',

  data: () => ({
    coins: [
      [
        { name: 'BTC', icon: '/images/btc.png' },
        { name: 'ETH', icon: '/images/eth.png' },
      ],
      [
        { name: 'USDT', icon: '/images/usdt.png' },
        { name: 'USDC', icon: '/images/usdc.png' },
      ],
    ],
  }),
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
