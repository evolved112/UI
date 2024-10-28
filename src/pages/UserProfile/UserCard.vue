<template>
  <card class="card-user">
    <div slot="image">
      <img src="@/assets/img/background.jpg" alt="..." />
    </div>
    <div>
      <div class="author">
        <img
          class="avatar border-white"
          src="@/assets/img/faces/face-2.jpg"
          alt="..."
        />
        <h4 class="title">
          User Name
          <br />
          <a href="#">
            <small>username@gmail.com</small>
          </a>
        </h4>
      </div>
    </div>
    <hr />
    <div class="text-center">
      <sidebar-link
        to="/login"
        type="button"
        round
        @click.native.prevent="updateProfile"
      >
        Log out
      </sidebar-link>
    </div>
  </card>
</template>
<script>
export default {
  data() {},
  methods: {
    getClasses(index) {
      var remainder = index % 3;
      if (remainder === 0) {
        return "col-lg-3 offset-lg-1";
      } else if (remainder === 2) {
        return "col-lg-4";
      } else {
        return "col-lg-3";
      }
    },
  },
};
</script>
<style></style>
