<template>
  <main class="container">
    <b-container fluid="sm">
      <b-col class="col-sm-3"></b-col>

      <b-col class="section">
        <b-form @submit="onSubmit" v-if="show" style="margin-top: 3rem">
          <h2>Add a New Product Owner</h2>

          <!--  Name Input  -->
          <b-form-group label="Owner" label-for="owner">
            <b-form-input
              v-model="name"
              placeholder="Owner of Product"
              size="sm"
              required
            ></b-form-input>
          </b-form-group>

          <!-- About Textarea -->
          <b-form-group
            label="About"
            label-for="about"
          >
            <b-form-textarea
              v-model="about"
              size="sm"
              placeholder="About Me"
            ></b-form-textarea>
          </b-form-group>

          <!-- Image -->
          <b-form-group label="Add Photo" label-for="photo">
            <b-form-file
              v-model="selectedFile"
              placeholder="Add a file or drop it here..."
              drop-placeholder="Drop image file here..."
              @change="onFileSelected"
            ></b-form-file>
            <p>{{ fileName }}</p>
          </b-form-group>

          <b-button type="submit" @click="onAddOwner" variant="primary"
            >Add Product Owner</b-button
          >
        </b-form>

        <div class="owners" v-for="owner in owners" :key="owner._id">
          <p>{{ owner.name }}</p>
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
      let response = await $axios.$get("http://localhost:3000/api/owners");
      return {
        owners: response.owners,
      };
    } catch (err) {
      console.log(err);
    }
  },
  data() {
    return {
      name: "",
      about: "",
      owners: [],
      selectedFile: null,
      fileName: "",
      show: true,
    };
  },
  methods: {
    onFileSelected(event) {
      event.preventDefault();
      this.selectedFile = event.target.files[0];
      console.log(this.selectedFile);
      this.fileName = event.target.files[0].name;
    },
    async onAddOwner() {
      let data = new FormData()
      data.append('name', this.name)
      data.append('about', this.about)
      data.append('photo', this.selectedFile, this.selectedFile.name)

      let result = await this.$axios.$post("http://localhost:8000/api/owners", data);
      this.owners.push({name: this.name});
      console.log(this.owners)
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
