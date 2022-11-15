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
              :updateTermHandler = "updateTermHandler"
          />
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import AddProducts from "@/components/add-products/AddProducts.vue";
import ProductsTable from "@/components/products-table/Products-table.vue";
export default {
  name: "App",
  components: {
    ProductsTable,
    AddProducts,
  },
  data() {
    return {
      products: [
        {
          id: 1,
          name: "Water",
          price: 200,
          store: "Market",
        },
        {
          id: 2,
          name: "Coca Cola",
          price: 400,
          store: "Cola market",
        },
        {
          id: 3,
          name: "Pepsi Cola",
          price: 450,
          store: "Pepsi market",
        },
      ],
      term: "",
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
      if (term.length == 0) {
        return arr
      }
      return arr.filter(item => item.name.toLowerCase().indexOf(term) > -1)
    },
    updateTermHandler(term) {
      this.term = term
    }
  },
};

</script>
<style scoped></style>
