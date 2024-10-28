<template>
  <div class="contact-us full-screen">
    <nav class="navbar navbar-ct-default" role="navigation-demo">
      <div class="container">
        <div class="navbar-header">
          <router-link :to="{ path: '/' }" class="navbar-brand"
            >Home</router-link
          >
        </div>

        <!-- Collect the nav links, forms, and other content for toggling -->
        <div class="collapse navbar-collapse" id="navigation-example-2">
          <ul class="nav navbar-nav navbar-right">
            <li>
              <router-link :to="{ path: '/' }">Home</router-link>
            </li>
          </ul>
        </div>
        <!-- /.navbar-collapse -->
      </div>
      <!-- /.container-->
    </nav>

    <div class="wrapper wrapper-full-page section content">
      <div class="">
        <div class="container">
          <h2 class="text-center">Login</h2>
          <p class="text-center pb-3">
            Enter your username and password to login
          </p>
          <div class="login">
            <div>
              <form @submit.prevent="login">
                <div class="form-group">
                  <label for="username">Username</label>
                  <input
                    v-model="username"
                    type="text"
                    id="username"
                    required
                  />
                </div>
                <div class="form-group">
                  <label for="password">Password</label>
                  <input
                    v-model="password"
                    type="password"
                    id="password"
                    required
                  />
                </div>

                <p>
                  Don't have an account?<router-link
                    :to="{ path: '/dashboard' }"
                  >
                    Register Now!</router-link
                  >
                </p>
                <button type="submit" style="background-color: #68b3c8">
                  Login
                </button>

                <p v-if="errorMessage" class="error">{{ errorMessage }}</p>
              </form>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style scoped>
.login {
  max-width: 500px;
  margin: auto;
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 8px;
  background-color: #f9f9f9;
}

.form-group {
  margin-bottom: 15px;
}

label {
  display: block;
  margin-bottom: 5px;
  text-align: left;
}

input {
  width: 100%;
  padding: 8px;
  box-sizing: border-box;
  border: 1px solid #1a1a1a;
  border-radius: 5px;
}

button {
  padding: 10px 20px;
  background-color: #919f88;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  width: 100%;
  margin-top: 10px;
}
button:hover {
  background-color: #627f62;
}
.error {
  color: red;
  margin-top: 10px;
}

p {
  padding-top: 10px;
}

@media (prefers-color-scheme: dark) {
  label {
    color: black;
  }
  input {
    background-color: white;
    color: black;
  }
}
</style>
