<template>
  <div class="home">
    <vue-dropzone v-show="!uploaded"
                  ref="myVueDropzone"
                  id="dropzone"
                  :options="dropzoneOptions"
                  @vdropzone-success="onUpload">
    </vue-dropzone>

    <div class="imgUpLoadContainer" v-show="uploaded">
      <img class="imgUpLoad" :src="imgUrl" alt="upload image" title="upload image"/>
      <div class="dz-remove-upload" @click="reUpload">Upload</div>
    </div>
    <ul class="predict-result">
      Predict:
      <li v-for="item in predict" :key="item" class="predict-item">
        {{item}}
      </li>
    </ul>
    <ul class="predict-with-bem-result">
      Predict with Bem:
      <li v-for="item in predictWithBeamSearch" :key="item" class="predict-with-bem-item">
        {{item}}
      </li>
    </ul>
  </div>
</template>
<style>
@import url("https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css");

.vue-dropzone {
  width: 204px;
  margin: 0 auto;
  padding: 0;
  height: 204px;
}

.dropzone .dz-preview {
  margin: 0;
}

.dropzone .dz-message {
  margin-top: calc(50% - 9px);
}

.predict-result,
.predict-with-bem-result {
  width: 100%;
  text-align: left;
  text-transform: uppercase;
  font-weight: bold;
}

.predict-with-bem-result {
  color: #42b983;
}

.predict-with-bem-item,
.predict-item {
  text-transform: lowercase;
  font-weight: normal;
  margin-left: 3em;
}

.dz-remove {
  width: 80% !important;
  margin-left: 18px !important;
}

.imgUpLoadContainer {
  margin: 0 auto 3em auto;
  position: relative;
  width: 50%;
}

.dz-remove-upload {
  transition: opacity 0.3s ease-in-out;
  color: #fff;
  position: absolute;
  z-index: 30;
  margin-left: calc(50% - 30px);
  padding: 10px;
  top: inherit;
  bottom: 15px;
  border: 2px white solid;
  text-decoration: none;
  text-transform: uppercase;
  font-size: 0.8rem;
  font-weight: 800;
  letter-spacing: 1.1px;
  opacity: 0;
}

.imgUpLoadContainer:hover .dz-remove-upload {
  opacity: 1;
  cursor: pointer;
}

.imgUpLoad {
  width: 100%;
}
</style>
<script>
// @ is an alias to /src
import vue2Dropzone from "vue2-dropzone";
import "vue2-dropzone/dist/vue2Dropzone.min.css";
import DetailView from "../components/DetailView";

export default {
  name: "Upload",
  components: {
    DetailView,
    vueDropzone: vue2Dropzone
  },
  data: function() {
    return {
      uploaded: false,
      imgUrl: "",
      predict: [],
      predictWithBeamSearch: [],
      dropzoneOptions: {
        url:
          "http://janison2.southeastasia.cloudapp.azure.com:8000/predictbinary",
        maxFilesize: 500,
        createImageThumbnails: true,
        addRemoveLinks: true,
        headers: { "My-Awesome-Header": "header value" },
        dictDefaultMessage: "<i class='fa fa-cloud-upload'></i>UPLOAD ME"
      }
    };
  },
  methods: {
    onUpload: function(file, respond) {
      console.log(file);
      this.imgUrl = file.dataURL;
      this.predict = respond.predict;
      this.predictWithBeamSearch = respond.predict_with_beam_search;
      this.uploaded = true;
    },
    reUpload: function() {
      this.uploaded = false;
      this.$refs.myVueDropzone.removeAllFiles();
    }
  }
};
</script>
