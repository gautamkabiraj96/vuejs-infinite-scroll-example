<template>
  <div id="app">
    <div class="np-credits">wwww.nightprogrammer.com</div>
    <h1>Infinite scroll example</h1>
    <div
      v-infinite-scroll="loadMoreItems"
      infinite-scroll-disabled="isLoading"
      infinite-scroll-distance="10"
    >
      <div v-for="(item, i) of itemsList" :key="i" class="np-item">
        {{ item.id }}
      </div>
    </div>
    <div v-if="isLoading">Loading...</div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      itemsList: [],
      isLoading: false,
    };
  },
  methods: {
    loadMoreItems() {
      this.isLoading = true;
      setTimeout(() => {
        this.itemsList = [
          ...this.itemsList,
          ...Array(10)
            .fill()
            .map(() => {
              return { id: parseInt((Math.random() * 10000).toString(), 10) };
            }),
        ];
        this.isLoading = false;
      }, 500);
    },
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  padding: 24px;
}

.np-credits {
  font-size: 12px;
  margin-top: 12px;
  color: #4b4b4b;
}

.np-item {
  padding: 10px;
  border: 1px solid rgb(255, 83, 232);
  margin: 10px 0;
}
</style>