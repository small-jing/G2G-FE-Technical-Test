<template>
  <b-card :title="item.name" class="mb-2">
    <b-card-text>
      <b-row>
        <b-col cols="6">
          {{ item.category }}&nbsp;&nbsp;&nbsp;&nbsp;RM{{ item.price }}
        </b-col>
        <b-col cols="6">
          <div class="d-flex justify-content-end">
            <i
              v-if="!isWishlist"
              :class="['fas', 'fa-heart', 'wishlist-icon']"
              @click="addToWishlist"
            ></i>
            <i
              v-if="isWishlist"
              :class="['fas', 'fa-check-square', 'wishlist-icon']"
              @click="addToWishlist"
            ></i>
          </div>
        </b-col>
      </b-row>
    </b-card-text>
  </b-card>
</template>

<script>
export default {
  data() {
    return {
      isWishlist: false,
    };
  },
  props: {
    item: {
      type: Object,
      default: null,
    },
  },
  methods: {
    addToWishlist() {
      this.isWishlist = !this.isWishlist;
    },
  },
};
</script>

<style scoped>
.wishlist-icon {
  cursor: pointer;
  color: #e44d26;
  font-size: 20px;
}

.filled {
  color: red;
}
</style>
