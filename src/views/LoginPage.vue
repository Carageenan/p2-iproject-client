<template>
  <div
    class="hero min-h-screen bg-fixed"
    style="background-image: url(https://wallpaperaccess.com/full/1567736.png)"
  >
    <div class="hero-content flex-col lg:flex-row-reverse">
      <div class="text-center lg:text-left">
        <h1 class="text-5xl font-bold">Welcome Foodies!</h1>
        <p class="py-6">
          <span style="font-bold">FastOrder</span> is a website that'll make
          your customer's eating experience more convenient.
        </p>
        <p class="py-2">
          Do not have any account yet? You can register
          <button
            @click="changePage('/register')"
            type="button"
            style="text-decoration: underline"
          >
            here
          </button>
        </p>
      </div>
      <div class="card flex-shrink-0 w-full max-w-sm shadow-2xl bg-base-100">
        <div class="card-body">
          <form @submit.prevent="login">
            <div class="form-control">
              <label class="label">
                <span class="label-text">Email</span>
              </label>
              <input
                v-model="email"
                type="email"
                placeholder="email"
                class="input input-bordered"
              />
            </div>
            <div class="form-control">
              <label class="label">
                <span class="label-text">Password</span>
              </label>
              <input
                v-model="password"
                type="password"
                placeholder="password"
                class="input input-bordered"
              />
            </div>
            <div class="form-control mt-6">
              <button class="btn btn-primary">Login</button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "loginComp",
  data() {
    return {
      email: "",
      password: "",
    };
  },
  methods: {
    async login() {
      await this.$store.dispatch("doLoginResto", {
        email: this.email,
        password: this.password,
      });
      if (this.restaurantIsLogin) {
        this.$router.push(`/restaurant`);
      }
    },
    changePage(page) {
      this.$router.push(page);
    },
  },
  computed: {
    restaurantIsLogin() {
      return this.$store.state.restaurantIsLogin;
    },
    restoId() {
      return this.$store.state.restoId;
    },
  },
  created() {
    this.$store.commit("CHANGE_IN_LOGIN_PAGE_OR_REGISTER", true);
  },
};
</script>

<style>
</style>