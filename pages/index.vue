<template>
  <div class="container">
    <input type="text" v-model="comment" />
    <input type="radio" v-model="algorithm" id="alg1" value="alg1" />
    <label for="alg1">alg1</label>
    <input type="radio" v-model="algorithm" id="alg2" value="alg2" />
    <label for="alg2">alg2</label>

    <select v-model="percentage">
      <option disabled value="">Please select percentage</option>
      <option>20</option>
      <option>30</option>
      <option>40</option>
    </select>

    <button @click="submit">submit</button>

    {{ comment }}
    {{ algorithm }}
    {{ percentage }}
  </div>
</template>

<script>
export default {
  data() {
    return {
      comment: "",
      algorithm: "",
      percentage: ""
    };
  },
  methods: {
    async submit() {
      const { comment, algorithm, percentage } = this;
      const data = {
        comment,
        algorithm,
        percentage
      };
      const { result } = await this.$axios.$post("backend url", data);
    }
  }
};
</script>

<style lang="scss" scoped>
// stylehat
</style>
