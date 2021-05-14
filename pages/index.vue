<template>
  <div>
    <ul v-if="lista">
      <li v-for="item in lista" :key="item.slug">
        <nuxt-link :to="item.slug">{{ item.name }}</nuxt-link>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data: () => ({
    lista: null,
  }),

  mounted: async function () {
    let response = await this.$axios.get(
      "https://api.ohmydoce.com.br/api/public/products"
    );
    this.lista = response.data.data.data;
  },
};
</script>

<style>
</style>
