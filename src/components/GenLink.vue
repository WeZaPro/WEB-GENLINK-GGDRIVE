<template>
  <div class="mt-10">
    <h5>{{ msg }}</h5>
  </div>

  <v-sheet class="mx-auto mt-20" max-width="600">
    <v-form validate-on="submit lazy" @submit.prevent="submit">
      <v-text-field
        v-model="getGoogleLink"
        :rules="rules"
        bg-color="#FFF3E0"
        label="LINK FROM GOOGLE DRIVE SHARING"
      ></v-text-field>

      <v-btn
        :loading="loading"
        class="mt-2"
        text="GENERATE LINK"
        color="#F44336"
        type="submit"
        block
      ></v-btn>
      <!-- <div class="mt-10">preview url : {{ results }}</div> -->
      <v-text-field
        class="mt-10"
        v-model="results"
        :rules="rules"
        bg-color="#E3F2FD"
        label="PREVIEW IMAGE URL"
        :disabled="true"
      ></v-text-field>
      <div>
        <v-btn
          :loading="loading"
          class="mt-2"
          text="COPY LINK TO CLIPBOARD"
          color="#9C27B0"
          block
          @click="copyURL"
        ></v-btn>
        <v-btn
          :loading="loading"
          class="mt-2"
          text="PREVIEW IMAGE URL"
          color="#2196F3"
          block
          @click="getImage"
        ></v-btn>
        <v-img
          class="mt-5"
          :width="600"
          aspect-ratio="9/9"
          cover
          :src="previewImage"
        ></v-img>
      </div>
    </v-form>
  </v-sheet>
</template>
<script>
export default {
  props: {
    msg: String,
  },
  data: (vm) => ({
    disableCheck: false,
    loading: false,
    rules: [(value) => vm.checkApi(value)],
    timeout: null,
    getGoogleLink: "",
    results: "",
    previewImage: "",
  }),

  methods: {
    async copyURL() {
      console.log("results--> ", this.results);

      if (!this.results) {
        alert("ไม่มีข้อมูล!");
      } else {
        try {
          await navigator.clipboard.writeText(this.results);
          alert("Copied link to clipboard !!! ");
        } catch ($e) {
          alert("Cannot copy");
        }
      }
    },
    getImage() {
      this.previewImage = this.results;
      console.log(" this.previewImage ---> ", this.previewImage);
    },
    async submit(event) {
      console.log("event---> ", event);
      console.log("getGoogleLink---> ", this.getGoogleLink);
      if (this.getGoogleLink) {
        // sample
        // https://drive.google.com/file/d/1mDsxLfKeTLAnioe4rVzjue2z0Ap9lDu9/view?usp=sharing
        let message = this.getGoogleLink;
        let arr = message.split("/");

        console.log("arr---> ", arr.length);
        if (arr.length !== 7) {
          alert("Link ไม่ถูกต้อง");
        } else {
          const idImage = arr[5];
          this.results = `https://drive.google.com/thumbnail?sz=w1000&id=${idImage}`;
          this.loading = true;
          const results = await event;
          this.loading = false;
        }
      } else {
        alert("Please input link");
      }

      //   alert(JSON.stringify(results, null, 2));
    },
    async checkApi(userName) {
      return new Promise((resolve) => {
        clearTimeout(this.timeout);

        this.timeout = setTimeout(() => {
          if (!userName) return resolve("Please enter a user name.");
          if (userName === "johnleider")
            return resolve("User name already taken. Please try another one.");

          return resolve(true);
        }, 1000);
      });
    },
  },
};
</script>
