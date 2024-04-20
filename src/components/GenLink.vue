<template>
  <h3>{{ msg }}</h3>
  <v-sheet class="mx-auto" max-width="600">
    <v-form validate-on="submit lazy" @submit.prevent="submit">
      <v-text-field
        v-model="getGoogleLink"
        :rules="rules"
        label="GOOGLE LINK"
      ></v-text-field>

      <v-btn
        :loading="loading"
        class="mt-2"
        text="GENERATE LINK"
        type="submit"
        block
      ></v-btn>
      <!-- <div class="mt-10">preview url : {{ results }}</div> -->
      <v-text-field
        class="mt-10"
        v-model="results"
        :rules="rules"
        label="PREVIEW IMAGE URL"
      ></v-text-field>
      <div>
        <v-img
          class="mt-5"
          :width="600"
          aspect-ratio="9/9"
          cover
          :src="previewImage"
        ></v-img>
        <v-btn
          :loading="loading"
          class="mt-2"
          text="PREVIEW IMAGE URL"
          block
          @click="getImage"
        ></v-btn>
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
    loading: false,
    rules: [(value) => vm.checkApi(value)],
    timeout: null,
    getGoogleLink: "",
    results: "",
    previewImage: "",
  }),

  methods: {
    getImage() {
      this.previewImage = this.results;
      console.log(" this.previewImage ---> ", this.previewImage);
    },
    async submit(event) {
      console.log("event---> ", event);
      console.log("getGoogleLink---> ", this.getGoogleLink);
      // sample
      // https://drive.google.com/file/d/1mDsxLfKeTLAnioe4rVzjue2z0Ap9lDu9/view?usp=sharing
      let message = this.getGoogleLink;
      let arr = message.split("/");

      console.log("arr---> ", arr);

      const idImage = arr[5];
      this.results = `https://drive.google.com/thumbnail?sz=w1000&id=${idImage}`;
      this.loading = true;

      const results = await event;

      this.loading = false;

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
