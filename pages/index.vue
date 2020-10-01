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
        <div>
          <a id="submit_btn" @click="submit">دیدن نتیجه</a>
        </div>
        <div v-if="result" class="result_box">
          <a>گروه احساسی تشخیص داده شده : </a>
          <a>{{ result['final'] }}</a>

        </div>
        <div class="container table_box" v-if="result">


          <div class="table ">

            <div>
              <a class="table_title">خشمگین</a>
              <a class="table_text">{{ result['Furious'] }}</a>
            </div>
            <div>
              <a class="table_title">عصبانی</a>
              <a class="table_text">{{ result['Angry'] }}</a>
            </div>
            <div>
              <a class="table_title">خنثی</a>
              <a class="table_text">{{ result['Neutral'] }}</a>
            </div>
            <div>
              <a class="table_title">خوشحال</a>
              <a class="table_text">{{ result['Happy'] }}</a>
            </div>
            <div>
              <a class="table_title">بسیار راضی</a>
              <a class="table_text">{{ result['Delighted'] }}</a>
            </div>

          </div>


        </div>
<!--        <span> {{ result }} </span>-->

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


  </div>
</template>

<script>
export default {
  data() {
    return {
      comment: "",
      classifier: 'NB',
      percentage: 25,
      result: null
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

      this.result = await this.$axios.$post("api/result", data);
      switch (this.result['final']) {
        case 0 :
          this.result['final'] = 'خنثی'
      }

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
  //background-color: bisque;
  display: inline-flex;
  width: 60%;
  overflow: hidden;
  flex-direction: row;
  margin-top: 12px;
  text-align: center;
  alignment: center;
  child-align: middle;
  align-content: center;
  align-items: flex-start;


}

.my_radio {
  //background-color: chocolate;
  display: inline-flex;
  color: #b30753;
  flex-direction: column;
  text-align: left;
  height: 100%;
  //alignment: center;
  //vertical-align: center;

}

.my_radio div {
  margin: 4px;
  //background-color: cadetblue;
}

.my_radio_2 div {
  direction: rtl;
  margin-left: 12px;

}

.comment_box {
  width: 68%;
  margin-top: 8px;
  direction: rtl;
  //background-color: chocolate;
}

#comment_text {
  background-color: #adabf5;
  box-shadow: 0 0 20px 0 rgba(0, 0, 0, 0.2), 0 5px 5px 0 rgba(0, 0, 0, 0.24);
  //box-shadow: 0 3px 6px rgba(0, 0, 0, .16);
  direction: rtl;
  border: none;
  outline: none;
  padding-right: 12px;
  padding-left: 12px;
  color: #2f2e2e;
  appearance: none;
  padding-top: 8px;
  line-height: 20px;
  font-size: larger;
}

#submit_btn {
  margin-top: 16px;
  padding: 4px 32px 8px 32px;
  border-radius: 5px;
  box-shadow: 0 3px 6px rgba(0, 0, 0, .21);
  //border-color: #b30753;
  color: #b30753;
  background-color: #fff;
  font-size: 15px;
  align-self: center;
  cursor: pointer;
  display: inline-block;
  transition: all .3s ease;
  text-decoration: none;
}

#submit_btn:hover {
  color: white;
  background: #b30753;
  border-color: #b30753;
}

.table_box {
  //background-color: burlywood;
  margin-top: 24px;
  //padding-right: 24px;
  //padding-left: 24px;
  width: 100%;
  display: inline-block;

}

.table {
  border: 4px solid black;
  direction: rtl;
  display: inline-flex;
  flex-direction: row;
  width: 80%;
}

.table div {
  display: inline-flex;
  flex-direction: column;
  height: content-box;
  //border-left: 1px solid black;
  //border-right: 1px solid black;
  //background-color: mediumseagreen;


  width: 20%;
}

.table_title {
  border-left: 1px solid black;
  border-right: 1px solid black;
  border-bottom: 1px solid black;
  padding-top: 4px;
  padding-bottom: 4px;
  background-color: mediumseagreen;
}

.table_text {
  border-top: 1px solid black;
  border-left: 1px solid black;
  border-right: 1px solid black;
  padding-top: 4px;
  padding-bottom: 4px;
  background-color: #adabf5;
  direction: ltr;
}

.result_box {
  //background-color: bisque;
  margin-top: 24px;
  text-align: right;
  padding: 12px 32px 12px 12px;
  margin-right: 32px;
  width: 80%;
}
</style>
