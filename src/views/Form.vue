<template>
  <div>
    <Header :cartItemCount="cartItemCount" />
    <div class="row">
      <div class="col-md-11 col-md-offset-1">
        <div class="panel panel-info">
          <div class="panel-heading">Pet Depot Checkout</div>
          <div class="panel-body">
            <div class="form-group">
              <div class="col-md-12">
                <h4>
                  <strong>Enter Your Information</strong>
                </h4>
              </div>

              <div class="form-group">
                <div class="col-md-6">
                  <strong>First Name:</strong>
                  <input v-model.trim="order.firstName" class="form-control" />
                </div>
                <div class="col-md-6">
                  <strong>Last Name:</strong>
                  <input v-model.trim="order.lastName" class="form-control" />
                </div>
              </div>

              <div class="form-group">
                <div class="col-md-12">
                  <strong>Address:</strong>
                </div>
                <div class="col-md-12">
                  <input v-model.trim="order.address" class="form-control" />
                </div>
              </div>

              <div class="form-group">
                <div class="col-md-12">
                  <strong>City:</strong>
                </div>
                <div class="col-md-12">
                  <input v-model.trim="order.city" class="form-control" />
                </div>
              </div>

              <div class="form-group">
                <div class="col-md-2">
                  <strong>State:</strong>
                  <select v-model="order.state" class="form-control">
                    <option disabled value>State</option>
                    <option v-for="(state, key) in states" :value="state" :key="state.id">{{key}}</option>
                  </select>
                </div>
              </div>

              <div class="form-group">
                <div class="col-md-6 col-md-offset-4">
                  <strong>Zip / Postal Code</strong>
                  <input v-model.number="order.zip" class="form-control" />
                </div>
              </div>

              <div class="form-group">
                <div class="col-md-6 boxes">
                  <input
                    type="checkbox"
                    id="gift"
                    value="true"
                    :true-value="order.sendGift"
                    :false-value="order.dontSendGift"
                    v-model="order.gift"
                  />
                  <label for="checkbox">Ship As Gift?</label>
                </div>
              </div>

              <div class="form-group">
                <div class="col-md-6 boxes">
                  <input type="radio" id="business" value="Business" v-model="order.method" />
                  <label for="business">Business</label>

                  <input type="radio" id="home" value="Home" v-model="order.method" />
                  <label for="home">Home</label>
                </div>
              </div>

              <div class="form-group">
                <div class="col-md-6">
                  <button
                    type="submit"
                    class="btn btn-primary submit"
                    v-on:click="submitForm"
                  >Place Order</button>
                </div>
              </div>

              <div class="col-md-12 verify">
                <pre>
                  First Name: {{order.firstName}}
                  Last Name: {{order.lastName}}
                  Address: {{order.address}}
                  City: {{order.city}}
                  Zip: {{order.zip}}
                  State: {{order.state}}
                  Method: {{order.method}}
                  Gift: {{order.gift}}

                </pre>
              </div>
            </div>
            <!-- end of global form-group -->
          </div>
        </div>
        <!-- end of panel-info -->
      </div>
    </div>
  </div>
</template>

<script>
import Header from "@/components/Header.vue";
export default {
  name: "Form",
  props: ["cartItemCount"],
  data() {
    return {
      states: {
        AL: "Alabama",
        AZ: "Arisona",
        CA: "Calofornia",
        NV: "Nevada",
        AK: "Alaska",
        IA: "Iowa"
      },
      order: {
        firstName: "",
        lastName: "",
        address: "",
        city: "",
        zip: "",
        state: "",
        method: "Business",
        gift: "Do Not Sand As A Gift",
        sendGift: "Sand As A Gift",
        dontSendGift: "Do Not Sand As A Gift"
      }
    };
  },

  components: { Header },

  methods: {
    submitForm() {
      console.log("Submitted");
    }
  }
};
</script>
