<template>
  <v-sheet class="mx-auto mt-15 dotted" max-width="600">
    <h3>ตัวอย่างการ COPY LINK จาก Google Drive</h3>
    <div class="border-lg mt-5">
      <v-img
        class="mt-2"
        :width="600"
        aspect-ratio="4/4"
        cover
        :src="a"
      ></v-img>
    </div>
    <div class="border-lg mt-5">
      <v-img
        class="mt-2"
        :width="600"
        aspect-ratio="4/4"
        cover
        :src="b"
      ></v-img>
    </div>
    <div class="border-lg mt-5">
      <v-img
        class="mt-2"
        :width="600"
        aspect-ratio="4/4"
        cover
        :src="c"
      ></v-img>
    </div>
    <div class="border-lg mt-5">
      <v-img
        class="mt-2"
        :width="600"
        aspect-ratio="4/4"
        cover
        :src="d"
      ></v-img>
    </div>
  </v-sheet>
</template>
<script>
import imgA from "../assets/0.png";
import imgB from "../assets/1.png";
import imgC from "../assets/2.png";
import imgD from "../assets/3.png";
export default {
  data() {
    return {
      a: imgA,
      b: imgB,
      c: imgC,
      d: imgD,
    };
  },
};
</script>
<style scope>
borderA {
  border: 5px solid red;
}
dotted {
  border-style: dotted;
}
</style>
