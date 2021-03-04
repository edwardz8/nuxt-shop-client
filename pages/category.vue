<template>
  <main class="container">
    <b-container fluid="sm">
      <b-col class="col-sm-3"></b-col>

      <b-col class="section">
        <b-form @submit="onSubmit" v-if="show" style="margin-top: 3rem">
          <h2>Add a New Category</h2>

          <!--  Category Type Input  -->
          <b-form-group label="Category Type" label-for="category-type">
            <b-form-input
              v-model="type"
              placeholder="Category Type"
              size="sm"
              required
            ></b-form-input>
          </b-form-group>

          <b-button type="submit" @click="onAddCategory" variant="primary"
            >Add Category</b-button
          >
        </b-form>

        <div class="categories" v-for="category in categories" :key="category._id">
          <p>{{ category.type }}</p>
        </div>
      </b-col>

      <b-col class="col-sm-3"></b-col>
    </b-container>
  </main>
</template>

<script>
export default {
  async asyncData({ $axios }) {
    try {
      let response = await $axios.$get("http://localhost:3000/api/categories");
    } catch (err) {
      console.log(err);
    }
  },
  data() {
    return {
      type: "",
      categories: [],
      show: true,
    };
  },
  methods: {
    async onAddCategory() {
      let data = { type: this.type };
      let result = await this.$axios.$post("http://localhost:8000/api/categories", data);
      this.categories.push(data);
    },
  },
};
</script>

<style scoped>
.section {
  margin: 0 auto;
  height: 100vh;
  display: flex;
  justify-content: center;
}
</style>
