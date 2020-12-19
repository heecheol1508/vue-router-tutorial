<template>
  <div>
    <h1>Users</h1>
    <h2>{{ $route.params }}</h2>
    <h2>{{ $route.query }}</h2>
  </div>
</template>

<script>
export default {
  computed: {
    userId() {
      return this.$route.params.userId;
    },
  },
};
</script>