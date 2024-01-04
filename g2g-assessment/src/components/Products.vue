<template>
  <div>
    <h2 class="mt-2 mb-2">Products</h2>
    <div class="mt-1 mb-1 rounded-div">
      <h4>Filter</h4>
      <b-form>
        <b-row>
          <b-col cols="3">
            <b-form-group label="Product Name:" label-for="input-1">
              <b-form-input
                type="text"
                placeholder="Enter product name"
                v-model="productName"
                required
              />
            </b-form-group>
          </b-col>
          <b-col cols="3">
            <b-form-group label="Product Category:" label-for="input-1">
              <b-form-select
                v-model="productCategory"
                :options="categoryOptions"
                value-field="text"
              ></b-form-select>
            </b-form-group>
          </b-col>
          <b-col cols="3">
            <b-form-group label="Sort by Price:" label-for="sort-by-price">
              <b-form-radio-group
                v-model="sortByPrice"
                :options="sortByPriceOptions"
                name="sort-by-price-options"
              ></b-form-radio-group>
            </b-form-group>
          </b-col>
          <b-col cols="3">
            <b-form-group label="Sort by Name:" label-for="sort-by-name">
              <b-form-radio-group
                v-model="sortByName"
                :options="sortByNameOptions"
                name="sort-by-name-options"
              ></b-form-radio-group>
            </b-form-group>
          </b-col>
        </b-row>
        <div class="mt-3 d-flex justify-content-end">
          <b-button type="reset" variant="danger" @click="resetFilter"
            >Reset</b-button
          >
        </div>
      </b-form>
    </div>
    <div class="mt-3">
      <b-row>
        <b-col cols="4" v-for="food in filteredFood" :key="food.id">
          <item-card :item="food" />
        </b-col>
      </b-row>
    </div>
  </div>
</template>

<script>
import ItemCard from "./ItemCard.vue";

export default {
  components: {
    ItemCard,
  },
  created() {},
  computed: {
    filteredFood() {
      let filtered = this.foods;

      if (this.productName) {
        filtered = this.foods.filter((food) =>
          food.name.toLowerCase().includes(this.productName.toLowerCase())
        );
      }

      if (this.productCategory) {
        filtered = this.foods.filter(
          (food) =>
            this.productCategory === "" ||
            food.category === this.productCategory
        );
      }

      if (this.sortByName) {
        filtered = filtered.sort((a, b) =>
          this.sortByName === "ascending"
            ? a.name.localeCompare(b.name)
            : b.name.localeCompare(a.name)
        );
      }

      if (this.sortByPrice) {
        filtered = filtered.sort((a, b) =>
          this.sortByPrice === "lowest" ? a.price - b.price : b.price - a.price
        );
      }

      return filtered;
    },
  },
  data() {
    return {
      productName: null,
      productCategory: null,
      sortByPrice: null,
      sortByName: null,
      foods: [
        {
          id: 1,
          name: "Nasi Lemak",
          category: "Main Dish",
          price: 5,
        },
        {
          id: 2,
          name: "Butter Milk Chicken",
          category: "Main Dish",
          price: 7,
        },
        {
          id: 3,
          name: "Pineapple Juice",
          category: "Beverage",
          price: 4,
        },
        {
          id: 4,
          name: "Pandan Layer Cake",
          category: "Dessert",
          price: 5,
        },
        {
          id: 5,
          name: "Coconut Shake",
          category: "Beverage",
          price: 8,
        },
        {
          id: 6,
          name: "Kampung Fried Rice",
          category: "Main Dish",
          price: 12,
        },
        {
          id: 7,
          name: "Onde-Onde",
          category: "Dessert",
          price: 15,
        },
      ],
      categoryOptions: [
        {
          value: "main-dishes",
          text: "Main Dish",
        },
        {
          value: "beverage",
          text: "Beverage",
        },
        {
          value: "dessert",
          text: "Dessert",
        },
      ],
      sortByPriceOptions: [
        { text: "Highest", value: "highest" },
        { text: "Lowest", value: "lowest" },
      ],
      sortByNameOptions: [
        { text: "Ascending", value: "ascending" },
        { text: "Descending", value: "descending" },
      ],
    };
  },
  methods: {
    resetFilter() {
      this.productName = null;
      this.productCategory = null;
      this.sortByPrice = null;
      this.sortByName = null;
    },
  },
};
</script>

<style scoped>
.rounded-div {
  border: 1px solid #ccc;
  border-radius: 10px;
  padding: 10px;
}
</style>
