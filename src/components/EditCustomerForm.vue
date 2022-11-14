<template>
  <b-form class="mt-3">
    <b-row>
      <b-row>
        <h4 class="text-secondary">Contact Details</h4>
      </b-row>
      <b-col cols="6">
        <b-form-group id="first-name" label="First Name" label-for="first-name">
          <b-form-input
              id="first-name"
              v-model="customer.contact_firstname"
              placeholder="First Name"
              type="text"
          ></b-form-input>
        </b-form-group>
      </b-col>
      <b-col cols="6">
        <b-form-group id="last-name" label="Last Name" label-for="last-name">
          <b-form-input
              id="last-name"
              v-model="customer.contact_lastname"
              placeholder="Last Name"
              type="text"
          ></b-form-input>
        </b-form-group>
      </b-col>
    </b-row>
    <b-row class="mt-3">
      <b-col cols="6">
        <b-form-group id="email" label="E-Mail" label-for="email">
          <b-form-input
              id="email"
              v-model="customer.contact_email"
              placeholder="example@crm.com"
              type="email"
          ></b-form-input>
        </b-form-group>
      </b-col>
    </b-row>
    <b-row class="mt-5">
      <h4 class="text-secondary">Company Details</h4>
    </b-row>
    <b-row>
      <b-col cols="4">
        <b-form-group
            id="company_name"
            label="Company Name"
            label-for="company_name"
        >
          <b-form-input
              id="company_name"
              v-model="customer.company_name"
              placeholder="XYZ Industries"
              type="text"
          ></b-form-input>
        </b-form-group>
      </b-col>
    </b-row>
    <b-row>
      <b-col cols="4">
        <b-form-group
            id="acquired_on"
            label="Acquired On"
            label-for="acquired_on"
        >
          <b-form-input
              id="acquired_on"
              v-model="customer.acquired_on"
              type="date"
          ></b-form-input>
        </b-form-group>
      </b-col>
    </b-row>
    <b-row class="mt-2">
      <b-form-checkbox
          id="customer_status"
          v-model="customer.customer_status"
          name="customer-status"
          unchecked-value="inactive"
          value="active"
      >
        Customer is active
      </b-form-checkbox>
    </b-row>
    <b-row class="mt-4">
      <b-col cols="3">
        <b-button class="px-5" variant="primary" @click="updateCustomer"
        >Update Customer
        </b-button
        >
      </b-col>
      <b-col>
        <b-button variant="warning" @click="triggerClose">Close</b-button>
      </b-col>
    </b-row>
  </b-form>
</template>

<script>
import axios from "axios";

export default {
  name: "CreateCustomerModal",
  props: {
    customerId: Number,
  },
  data() {
    return {
      customer: {},
    };
  },
  mounted() {
    this.getCusomterByID();
  },
  methods: {
    triggerClose() {
      this.$emit("closeEditModal");
    },
    getCusomterByID() {
      axios
          .get(`http://localhost:3000/customers/${this.customerId}`)
          .then((response) => {
            this.customer = response.data;
          })
          .catch((error) => {
            console.log(error);
          });
    },
    updateCustomer() {
      axios
          .put(
              `http://localhost:3000/customers/${this.customerId}`,
              this.customer
          )
          .then((response) => {
            console.log(response.data);
            this.$emit("closeEditModal");
            this.$emit("reloadDataTable");
            this.$emit("showSuccessAlert");
          })
          .catch((error) => {
            console.log(error);
          });
    },
  },
};
</script>