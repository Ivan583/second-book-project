<template>
  <div>
    <header>
      <div class="navbar navbar-default col-md-offset-1">
        <div class="navbar-header">
          <h1>
            <router-link to="Form" />
            {{sitename}}
          </h1>
        </div>
        <div class="nav navbar-nav navbar-right cart">
          <button type="button" class="btn btn-default btn-lg" @click="showCheckout">
            <span>{{ cartItemCount }}</span>
            <span class="glyphicon glyphicon-shopping-cart"></span> Checkout
          </button>
        </div>
      </div>
    </header>
  </div>
</template>

<script>
export default {
  name: "Header",
  data() {
    return {
      sitename: "Vue.js Pet Depot"
    };
  },
  props: ["cartItemCount"],
  methods: {
    showCheckout() {
      this.$router.push({ name: "Form" });
    }
  }
};
</script>
