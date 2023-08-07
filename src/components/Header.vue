<template>
     <div class="fixed top-0 left-0 z-50 w-full py-4" style="background-color:white;box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);">
          <div class="relative flex items-center py-2 mx-auto justify-between container  px-3 ">
            <div class="flex">
                <div 
                  class="sm:ml-0 flex items-center justify-start"
                >
                    <span
                    @click="$store.dispatch('goTo', '/')"
                    class="ml-3 text-2xl text-blue-900 font-bold hidden md:block"
             
                    >Country Catalog</span
                  >
                </div>
            </div>    
          </div>
      </div>

</template>

<script>
export default {
  data() {
    return {};
  },
  methods: {
    goTo(url) {
      this.$router.push(url);
    },
    logout() {
      localStorage.removeItem("token");
      this.$router.push("/");
      location.reload();
    },
  },
};
</script>

<style scoped>
.backcolor:hover {
  /* background-image: linear-gradient(to top, #84d5f0 0%, #8b9cd8 100%); */
  background-color: rgba(240, 255, 255, 0.267);
}

.router-link-exact-active {
  background-color: rgb(95, 209, 254);
}
</style>
