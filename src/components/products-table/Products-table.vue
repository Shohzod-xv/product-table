<template>
  <div class="card-body">
    <form @submit.prevent>
    <table class="table caption-top"  >
      <thead>
      <tr>
        <th scope="col">#</th>
        <th scope="col">
          <input
            type="text"
            class="form-control"
                placeholder="Product Name"
            :value="name"
            @input="name = $event.target.value"
        />
        </th>
        <th scope="col">
          <input
              type="number"
              class="form-control"
              placeholder="Product Price"
              :value="price"
              @input="price = $event.target.value"
          />
        </th>
        <th scope="col">
          <input
              type="text"
              class="form-control"
              placeholder="Product Store"
              :value="store"
              @input="store = $event.target.value" />
        </th>
        <th scope="col">
          <input
              type="submit"
              class="btn btn-outline-success add-submit"
              value="Qo'shish"
              @click="addProduct"
          />
        </th>
      </tr>

      <tr>
        <th scope="col">ID</th>
        <th scope="col">Product Name</th>
        <th scope="col">Product Price</th>
        <th scope="col">Product store</th>
        <th scope="col">####</th>
      </tr>
      </thead>
      <tbody v-for="product in products">
      <tr>
        <th scope="row">{{ product.id }}</th>
        <td>{{ product.name }}</td>
        <td>{{ product.price }}</td>
        <td>{{ product.store}}</td>
        <td>
          <button
              type="submit"
              class="btn btn-outline-danger btn sm"
              @click="$emit('onDelete',product.id)"
          ><i class="fas fa-trash"></i>
          </button>
        </td>
      </tr>
      </tbody>
      </table>
    </form>
  </div>
</template>

<script>
export default {
  name: "Products-table",
  props: {
    products: {
      type: Array,
      required: true,
    },
  },
  methods: {
    addProduct() {
      const product = {
        id: this.$parent.products.length + 1,
        name: this.name,
        price: this.price,
        store: this.store,
      };
      this.$emit("createProduct", product);
      this.name = "";
      this.price = "";
      this.store = "";
    },
  }
}
</script>

<style scoped>
.card {
  margin: 20px;
  padding: 6px;
}
tr:nth-child(even) {background-color: #f2f2f2;}
</style>
