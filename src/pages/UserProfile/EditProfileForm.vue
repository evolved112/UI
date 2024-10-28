<template>
  <card class="card" title="Edit Personal Information">
    <div>
      <form @submit.prevent>
        <div class="row">
          <div class="col-md-6">
            <fg-input
              type="text"
              label="First Name"
              placeholder="First Name"
              v-model="user.firstName"
            >
            </fg-input>
          </div>
          <div class="col-md-6">
            <fg-input
              type="text"
              label="Last Name"
              placeholder="Last Name"
              v-model="user.lastName"
            >
            </fg-input>
          </div>
        </div>

        <div class="row">
          <div class="col-md-6">
            <fg-input
              type="text"
              label="User Name"
              placeholder="User Name"
              v-model="user.username"
            >
            </fg-input>
          </div>
          <div class="col-md-6">
            <fg-input
              type="email"
              label="Email"
              placeholder="username@gmail.com"
              v-model="user.email"
            >
            </fg-input>
          </div>
        </div>

        <div class="text-center">
          <p-button type="info" round @click.native.prevent="updateProfile">
            Submit
          </p-button>
        </div>
        <div class="clearfix"></div>
      </form>
    </div>
  </card>
</template>
<script>
export default {
  data() {
    return {
      user: {
        username: "username",
        email: "username@gmail.com",
        firstName: "User",
        lastName: "Name",
      },
    };
  },
  methods: {
    updateProfile() {
      alert("Your data: " + JSON.stringify(this.user));
    },
  },
};
</script>
<style></style>
