<template>
  <img :src="require('../assets/' + img)" class="mx-auto"/>
  <div class="home text-center">
    <form @submit.prevent>
      <input type="file" @change="uploadBeforeSubmit" /> <br />
      <button
        class="border border-black px-2 py-1 mt-10"
        @click="uploadPicture"
      >
        Submit
      </button>
    </form>
  </div>
</template>

<script>
// @ is an alias to /src
// import axios from "axios";
export default {
  name: "Home",
  components: {},
  data() {
    return {
      selectedFile: null,
      img: "logo.png"
    };
  },
  methods: {
    async uploadPicture() {
      const fd = new FormData();
      fd.append("file", this.selectedFile, this.selectedFile.name);
      console.log(fd);
      // axios.post("http://localhost:9000/", fd).then(res => {
      //   console.log(res);
      // });
      const res = await fetch("http://localhost:9000/", {
        method: "POST",
        mode: "no-cors",
        body: fd
      });
      const data = await res;
      console.log(data);
    },

    uploadBeforeSubmit(event) {
      // console.log(event);
      this.selectedFile = event.target.files[0];
      console.log(this.selectedFile);
      // const fd = new FormData();
      // fd.append("file", this.selectedFile);
      // console.log(fd);
    }
  }
};
</script>
