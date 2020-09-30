<template>

  <div class="container my_main py-3">
    <div class="header">

    </div>
    <div class="container my_main_2">
      <div class="container my_radio"> <!-- algorithm radio buttons --->
        <div>
          <input type="radio" v-model="classifier" id="NB" value="NB" checked/>
          <label for="NB">Naive Bayes</label>
        </div>
        <div>
          <input type="radio" v-model="classifier" id="SVM" value="SVM"/>
          <label for="SVM">Support Vector Machine</label>
        </div>
        <div>
          <input type="radio" v-model="classifier" id="CNN" value="CNN"/>
          <label for="CNN">Convolution Neural Network</label>
        </div>


      </div>
      <div class="comment_box">
        <textarea cols="50" rows="6" id="comment_text" v-model="comment"
                  placeholder="متن خود را اینجا وارد کنید"/>
      </div>
      <div class="container my_radio my_radio_2">
        <div>
          <input type="radio" v-model="percentage" id="p10" value="10" checked/>
          <label for="p10">10%</label>
        </div>
        <div>
          <input type="radio" v-model="percentage" id="p20" value="20"/>
          <label for="p20">20%</label>
        </div>
        <div>
          <input type="radio" v-model="percentage" id="p25" value="25"/>
          <label for="p25">25%</label>
        </div>
        <div>
          <input type="radio" v-model="percentage" id="p30" value="30"/>
          <label for="p30">30%</label>
        </div>
        <div>
          <input type="radio" v-model="percentage" id="p40" value="40"/>
          <label for="p40">40%</label>
        </div>


      </div>


    </div>
    <div>

      <button id="submit_btn" @click="submit">submit</button>
    </div>
    <!--
        <div/>
        {{ comment }}
        {{ classifier }}
        {{ percentage }}
        <div/>
    -->


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
.header {
  height: 90px;
  background-color: cadetblue;
}

.my_main {
  width: 100%;
  background-color: #abc8ed;
  display: inline-block;
  text-align: center;
  alignment: center;
  child-align: middle;
  align-content: center;
  align-items: center;
  height: 100vh;

}

.my_main_2 {
  background-color: bisque;
  display: inline-flex;
  width: 60%;
  overflow: hidden;
  flex-direction: row;
  margin-top: 12px;
  //text-align: center;
  //alignment: center;
  //child-align: middle;
  //align-content: center;
  align-items: flex-start;


}

.my_radio {
  background-color: chocolate;
  display: inline-flex;
  color: #b30753;
  flex-direction: column;
  text-align: left;
  //alignment: center;
}

.my_radio div {
  margin: 4px;
  background-color: cadetblue;
}

.my_radio_2 div {
  direction: rtl;
  margin-left: 12px;

}

.comment_box {
  width: 68%;
  background-color: burlywood;
}

#comment_text {
  background-color: #66b398;
  direction: rtl;
  border: none;
  outline: none;
  padding-right: 12px;
  padding-left: 12px;
  color: #b30753;
  appearance: none;
  padding-top: 4px;
  line-height: 20px;
  font-size: larger;
}

#submit_btn {

}


</style>
