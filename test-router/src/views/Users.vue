<template>
  <div>
    <h1>Users</h1>
    <h2>{{ userId }}</h2>
  </div>
</template>

<script>
export default {
  computed: {
    userId() {
      return this.$route.params.userId;
    },
  },
  created() {
    console.log("router", this.$router);
    console.log("route", this.$route);
  },
};
</script>