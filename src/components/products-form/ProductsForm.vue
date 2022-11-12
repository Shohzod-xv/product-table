<template>
  <div class="card">
    <div class="card-body">
      <form @submit.prevent>
        <div class="row g-3 align-items-center">
          <div class="col-auto">
            <label class="col-form-label">Product Name</label>
            <input type="text" class="form-control" :value="name" @input="name = $event.target.value" />
          </div>
          <div class="col-auto">
            <label class="col-form-label">Product Price</label>
            <input type="number" class="form-control" :value="price" @input="price = $event.target.value" />
          </div>
          <div class="col-auto">
            <label class="col-form-label">Product store</label>
            <input type="text" class="form-control" :value="store" @input="store = $event.target.value" />
          </div>
          <div class="col-center">
            <input
              type="submit"
              class="btn btn-dark add-submit"
              value="Qo'shish"
              @click="addProduct"
            />
          </div>
        </div>
      </form>
    </div>
  </div>
</template>
<script>
export default {
  name: "ProductsForm",
  methods: {
    addProduct() {
      const product = {
        id: this.$parent.products.length + 1,
        name: this.name,
        price: this.price,
        store: this.store,
      };
      this.$emit("createProduct", product);
    },
  },
};
</script>

<style scoped>
.col-form-label {
  display: flex;
  justify-content: center;
  color: black;
  font-weight: bold;
}
.card {
  margin: 20px;
  padding: 6px;
}
</style>
