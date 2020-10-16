<template>
  <div>
    <Header :cartItemCount="cartItemCount" />
    <div v-for="product in sortedProducts" :key="product.id">
      <div class="row">
        <div class="col-md-4 col-md-offset-1">
          <figure>
            <img class="product" v-bind:src="product.image" />
          </figure>
        </div>

        <div class="col-md-6 col-md-offset-1 description">
          <h1 v-text="product.title"></h1>
          <p v-html="product.description"></p>
          <p class="price">{{ product.price | formatPrice }}</p>
          <div class="button">
            <button
              class="btn btn-primary btn-lg"
              @click="addToCart(product)"
              v-if="canAddToCart(product)"
            >
              Add to
              cart
            </button>
            <button disabled="true" class="btn btn-danger btn-lg" v-else>Impossible</button>

            <div>
              <span
                class="inventory-message"
                v-if="product.availableInventory - cartCount(product.id) === 0"
              >All Out!</span>
              <span
                class="inventory-message"
                v-else-if="product.availableInventory - cartCount(product.id) < 5"
              >Only {{ product.availableInventory - cartCount(product.id) }} left!</span>
              <span class="inventory-message" v-else>Buy Now!</span>
            </div>

            <div class="rating">
              <span :class="{'rating-active': checkRating(n, product)}" v-for="n in 5" :key="n.id">☆</span>
            </div>
          </div>
        </div>
      </div>
      <!-- end of row -->
      <hr />
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Header from "@/components/Header.vue";

export default {
  name: "Main",
  data() {
    return {
      products: [],
      cart: []
    };
  },

  components: {
    Header
  },

  methods: {
    checkRating(n, myProduct) {
      return myProduct.rating - n >= 0;
    },

    addToCart(aProduct) {
      this.cart.push(aProduct.id);
    },

    canAddToCart(aProduct) {
      return aProduct.availableInventory > this.cartCount(aProduct.id);
    },

    cartCount(id) {
      let count = 0;
      for (let i = 0; i < this.cart.length; i++) {
        if (this.cart[i] === id) {
          count++;
        }
      }
      return count;
    }
  },

  computed: {
    cartItemCount() {
      return this.cart.length || "";
    },
    sortedProducts() {
      if (this.products.length > 0) {
        let productArray = this.products.slice(0);

        function compare(a, b) {
          if (a.title.toLowerCase() < b.title.toLowerCase()) return -1;
          if (a.title.toLowerCase() > b.title.toLowerCase()) return 1;
          return 0;
        }
        return productArray.sort(compare);
      }
    }
  },

  filters: {
    formatPrice(price) {
      if (price > 999.99) {
        var priceString = price.toFixed(2);
        var priceArray = priceString.split("").reverse();
        var index = 3;
        while (priceArray.length > index + 3) {
          priceArray.splice(index + 3, 0, " ");
          index += 4;
        }
        return "$ " + priceArray.reverse().join("");
      } else {
        return "$ " + price.toFixed(2);
      }
    }
  },

  mounted() {
    fetch("/products.json")
      .then(res => res.json())
      .then(data => {
        this.products = data.products;
      })
      .catch(err => {
        console.log(err);
      });
  }
};
</script>
