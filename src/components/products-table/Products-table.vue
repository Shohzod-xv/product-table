<template>
  <div class="card">
  <div class="card-body">
    <form @submit.prevent>
      <span>
        <div class="card-header d-flex justify-content">
          <h4>Products table</h4>
          <div class="card-header-action">
            <form>
              <div class="input-group">
                <input
                    type="text"
                    class="form-control"
                    placeholder="Search"
                    :value="term"
                    @input="changeHandler"
                />
                <div class="input-group-btn">
                  <button class="btn btn-outline-dark"><i class="fas fa-search"></i></button>
                </div>
              </div>
            </form>
          </div>
        </div>
      </span>

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
              class="btn btn-outline-dark add-submit"
              value="+ Add"
              @click="addProduct"
          />
        </th>
      </tr>

      <tr>
        <th scope="col">ID</th>
        <th scope="col">Product Name</th>
        <th scope="col">Product Price</th>
        <th scope="col">Product store</th>
        <th scope="col">Delete</th>
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
              class="btn btn-outline-warning btn sm"
              @click="$emit('onDelete',product.id)"
          ><i class="fas fa-trash"></i>
          </button>
        </td>
      </tr>
      </tbody>
      </table>
    </form>
  </div>
  </div>
</template>
<script>
export default {
  name: "Products-table",
  props: {
    updateTermHandler: {
      type: Function,
      required: true,
    },
    products: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      term: "",
    };
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
    changeHandler(e) {
      this.term = e.target.value;
      this.updateTermHandler(this.term);
    },
  }
}
</script>

<style scoped>
.card {
  margin: 20px;
  padding: 6px;
}
tr:nth-child(even) {
  background-color: #030303;
  color: white;
}
.d-flex {
   display: -ms-flexbox!important;
   display: flex!important;
}
.justify-content {
   -ms-flex-pack: justify!important;
   justify-content: space-between!important;
}
.card-header{
  background-color: aliceblue;
  color: #030303;
}
</style>
