<template>
  <div class="app">
    <div class="container">
      <div class="row">
        <div class="col-12">
          <AddProducts />
          <ProductsTable
            :products="onSearchHandler(products, term)"
            @createProduct="createProduct"
            @onDelete="onRemoveHandler"
            :updateTermHandler="updateTermHandler"
          />
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import AddProducts from "@/components/add-products/AddProducts.vue";
import ProductsTable from "@/components/products-table/Products-table.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    ProductsTable,
    AddProducts,
  },
  data() {
    return {
      products: [],
      term: "",
      filter: "all",
    };
  },
  methods: {
    createProduct(item) {
      this.products.push(item);
    },
    onRemoveHandler(id) {
      this.products = this.products.filter((item) => item.id !== id);
    },
    onSearchHandler(arr, term) {
      if (term.length === 0) {
        return arr;
      }
      return arr.filter((item) => item.name.toLowerCase().indexOf(term) > -1);
    },
    updateTermHandler(term) {
      this.term = term;
    },
    async fetchProducts() {
      try {
        const { data } = await axios.get(
          "https://jsonplaceholder.typicode.com/posts?_limit=10"
        );
        this.products = data.map((item) => {
          return {
            id: item.id,
            name: item.title,
            price: item.id * 100,
            store: "Market",
          };
        });
      } catch (error) {
        alert(error.message);
      }
    },
  },
  mounted() {
    this.fetchProducts();
  },
};
</script>
<style scoped></style>
