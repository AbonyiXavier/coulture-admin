<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-sm-3"></div>
      <div class="col-sm-6">
        <div class="a-spacing-top-medium">
          <h2 class="text-center">Add new Product</h2>
          <form>
            <!-- Title -->
            <div class="a-spacing-top-medium">
              <label>Title</label>
              <input
                type="text"
                class="a-input-text"
                style="width:100%"
                v-model="title"
              />
            </div>
            <!-- Price Input-->
            <div class="a-spacing-top-medium">
              <label>Price</label>
              <input
                type="number"
                class="a-input-text"
                style="width:100%"
                v-model="price"
              />
            </div>
            <!-- stockQuantity input -->
            <div class="a-spacing-top-medium">
              <label>Stock Quantity</label>
              <input
                type="number"
                class="a-input-text"
                style="width:100%"
                v-model="stockQuantity"
              />
            </div>
            <!-- Description Textarea-->
            <div class="a-spacing-top-medium">
              <label>Description</label>
              <textarea
                type="text"
                placeholder="Provide Product Description"
                class="a-input-text"
                style="width:100%"
                v-model="description"
              ></textarea>
            </div>
            <!-- Photo file -->
            <div class="a-spacing-top-medium">
              <label style="margin-bottom: 0px">Add Photo</label>
              <div class="a-row a-spacing-top-medium">
                <label class="choosefile-button">
                  <i class="fal fa-plus"></i>
                  <input type="file" @change="onFileSelected" />
                  <p style="margin-top: -70px;">{{ fileName }}</p>
                </label>
              </div>
            </div>
            <hr />
            <!-- Button -->
            <div class="a-spacing-top-large">
              <span class="a-button-register">
                <span class="a-button-inner">
                  <span class="a-button-text" @click="onAddProduct"
                    >Add product</span
                  >
                </span>
              </span>
            </div>
          </form>
        </div>
      </div>
      <div class="col-sm-3"></div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: "",
      price: 0,
      description: "",
      selectedFile: null,
      stockQuantity: 1,
      fileName: "",
    };
  },
  methods: {
    onFileSelected(event) {
      this.selectedFile = event.target.files[0];
      console.log(this.selectedFile);
      this.fileName = event.target.files[0].name;
    },
    async onAddProduct() {
      let data = new FormData();
      data.append("title", this.title);
      data.append("price", this.price);
      data.append("description", this.description);
      data.append("stockQuantity", this.stockQuantity);
      data.append("photo", this.selectedFile, this.selectedFile.name);

      let result = await this.$axios.$post(
        "https://coulture-backend.herokuapp.com/api/products",
        data
      );

      this.$router.push("/");
    },
  },
};
</script>

<style></style>
