<template>
	<div>
		<span v-if="data">{{data.name}}</span>
	</div>
</template>

<script>
export default {
	data: () => ({
		data: null,
	}),

	head() {
		return {
			title: this.data ? this.data.name : null,
			meta: [
				{
					hid: "description",
					name: "description",
					content: this.tagDescription,
				},
			],
		};
	},

  async asyncData(context) {
    try {
      const response = await context.$axios.get(`https://api.ohmydoce.com.br/api/public/products/slug/${context.params.slug}`
      );
      let data = response.data.data;
      return {
        data,
      };
    } catch (error) {
      console.log(error)
    }
  },

	// mounted: async function () {
	// 	let response = await this.$axios.get(
	// 		"http://api.ohmydoce.com.br/api/public/products/slug/" +
	// 			this.$route.params.slug
	// 	);
	// 	this.data = response.data.data;
	// },

	computed: {
		tagDescription() {
			return this.data ? this.data.name : null;
		},
	},
};
</script>

<style>
</style>
