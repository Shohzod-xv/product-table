<template>
  <div class="card-body">
    <table class="table caption-top" >
      <thead>
      <tr>
        <th scope="col">ID</th>
        <th scope="col">Product Name</th>
        <th scope="col">Product Price</th>
        <th scope="col">Product store</th>
      </tr>
      </thead>
      <tbody v-for="product in products">
      <tr>
        <th scope="row">{{ product.id }}</th>
        <td>{{ product.name }}</td>
        <td>{{ product.price }}</td>
        <td>{{ product.store}}</td>
      </tr>
      </tbody>
    </table>
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
}
</script>

<style scoped>
.card {
  margin: 20px;
  padding: 6px;
}
</style>
