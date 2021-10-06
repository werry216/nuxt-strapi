<template>
<Products :products="products" :error="error" :storeUrl="storeUrl" />
</template>

<script>
import Products from "~/components/Products.vue"

export default {
  data() {
    return {
      products: [],
      storeUrl: process.env.storeUrl,
      error: null
    }
  },
  // async mounted() {
  //   try {
  //     this.products = await this.$strapi.$products.find(this.$i18n.locale)
  //   } catch (error) {
  //     this.error = error
  //   }
  // },
  // this didn't work: 
  // async mounted() {
  //   try {
  //     this.products = await this.$strapi.$products.find(this.$i18n.locale)
  //   } catch (error) {
  //     this.error = error
  //   }
  // },
  async asyncData ({$strapi, i18n }) {    
    const products = await $strapi.$products.find({_locale: i18n.locale })
    return {
      products
    }
  },

  components: {
    Products
  }
};
</script>
