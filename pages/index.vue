<template>
  <div class="container">
    <input type="text" v-model="comment"/>
    <input type="radio" v-model="classifier" id="NB" value="NB"/>
    <label for="alg1">alg1</label>
    <input type="radio" v-model="classifier" id="SVM" value="SVM"/>
    <label for="alg2">alg2</label>
    <input type="radio" v-model="classifier" id="CNN" value="CNN"/>
    <label for="alg2">alg3</label>

    <select v-model="percentage">
      <option disabled value="">Please select percentage</option>
      <option>10</option>
      <option>20</option>
      <option>25</option>
      <option>30</option>
      <option>40</option>
    </select>

    <button @click="submit">submit</button>
    <div/>
    {{ comment }}
    {{ classifier }}
    {{ percentage }}
    <div/>



  </div>
</template>

<script>
export default {
  data() {
    return {
      comment: "",
      classifier: "",
      percentage: ""
    };
  },
  methods: {
    async submit() {
      const {comment, classifier, percentage} = this;
      const data = {
        comment,
        classifier,
        percentage
      };
      const result = await this.$axios.$post("api/result", data);

      console.log(result)


    }
  }
};
</script>

<style lang="scss" scoped>
// stylehat
</style>
