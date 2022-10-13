<template>
  <div id="app">
    <h1>Vue Update image</h1>
    <div v-if="!imageFileUrl" class="uploader-wrapper">
      <div class="image-dropzone" @click="chooseImage">
        <p>Click to Upload</p>
      </div>
      <input
        type="file"
        style="display: none"
        ref="imageInput"
        accept="image/png,image/jpeg,image/jpg"
        @change="handleImageChoosen"
      />
    </div>
    <div v-else class="image-wrapper">
      <img width="320" :src="imageFileUrl" class="uploaded-image" />
      <button class="clear-button" @click="clearImage">Clear</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      imageFile: null,
      imageFileUrl: null,
    };
  },
  methods: {
    chooseImage() {
      this.$refs.imageInput.click();
    },
    handleImageChoosen(e) {
      const files = e.target.files;

      if (files[0] !== undefined) {
        if (files[0].name.lastIndexOf(".") <= 0) {
          return;
        }

        const fr = new FileReader();

        fr.readAsDataURL(files[0]);

        fr.addEventListener("load", () => {
          this.imageFileUrl = fr.result; // For DOM display purpose.
          this.imageFile = files[0]; // To be sent to server.
        });
      } else {
        this.clearImage();
      }
    },
    clearImage() {
      this.imageFile = null;
      this.imageFileUrl = null;
    },
  },
};

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

a,
button {
  color: #4fc08d;
}

button {
  background: none;
  border: solid 1px;
  border-radius: 2em;
  font: inherit;
  padding: 0.75em 2em;
  cursor: pointer;
  outline: none;
}

button:hover{
  color: red;
}

.uploader-wrapper,
.image-wrapper {
  margin: 50px auto;
}

.image-dropzone {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 320px;
  height: 240px;
  margin: 0 auto;
  border: 2px dashed #ccc;
  cursor: pointer;
}

.image-wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;

  .clear-button {
    margin-top: 30px;
  }
}
</style>
