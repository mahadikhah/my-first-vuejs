<template>
  <div>
    <div>
      <b-navbar toggleable="lg" type="dark" variant="info">
        <b-navbar-brand href="#">{{category}}</b-navbar-brand>

        <b-navbar-nav>
          <b-nav-item href="#" disabled>question {{index}}/10</b-nav-item>
        </b-navbar-nav>

        <!-- Right aligned nav items -->
      </b-navbar>
    </div>
  </div>
</template>
<script>
export default {
  name: "Header",
  props: {
    category: String,
    index: Number,
  },
};
</script>
<style scoped></style>