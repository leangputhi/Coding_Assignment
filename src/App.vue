<template>
  <div>
    <Header/>
    <RouterView />
  </div>
</template>

<script>
import { RouterView } from "vue-router";
import Header from "./components/Header.vue";
import jwt_decode from "jwt-decode";

export default {
  components: {
    Header,
  },
  data() {
    return {
      user: false,
    };
  },
  computed: {
    questions() {
      return $store.state.questions;
    },
  },
  created() {
    this.checkuser();
  },
  methods: {
    checkuser() {
      let token = localStorage.getItem("token");

      if (token == null) {
        this.user = false;
        this.$router.push("/");
      } else {
        this.user = true;

        this.$router.push("/Dashboard/Page");
      }
    },
  },
};
</script>

<style scoped></style>
