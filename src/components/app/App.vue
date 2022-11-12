<template>
  <div class="app">
    <div class="container">
      <div class="row">
        <div class="col-12">
          <AddProducts />
          <ProductsForm @createProduct="createProduct" />
          <ProductsTable :products="products" />
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import AddProducts from "@/components/add-products/AddProducts.vue";
import ProductsForm from "@/components/products-form/ProductsForm.vue";
import ProductsTable from "@/components/products-table/Products-table.vue";
export default {
  name: "App",
  components: {
    ProductsTable,
    AddProducts,
    ProductsForm,
  },
  data() {
    return {
      products: [
        {
          id: 1,
          name: "Product 1",
          price: 100,
          store: "Store 1",
        },
        {
          id: 2,
          name: "Product 2",
          price: 200,
          store: "Store 2",
        },
        {
          id: 3,
          name: "Product 3",
          price: 300,
          store: "Store 3",
        },
      ],
    };
  },
  methods: {
    createProduct(item) {
      this.products.push(item);
    },
  },
};
</script>
<style scoped></style>
