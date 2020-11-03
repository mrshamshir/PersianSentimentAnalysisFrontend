<template>
  <div class="container my_main py-3">
    <div class="container my_main_2">
      <div class="container flex-1 my_radio">
        <!-- algorithm radio buttons --->
        <div>الگوریتم انتخابی</div>
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
        <textarea
            cols="50"
            rows="10"
            id="comment_text"
            v-model="comment"
            :resizable="false"
            placeholder="متن خود را اینجا وارد کنید"
        />
        <a id="submit_btn" @click="submit">دیدن نتیجه</a>
        <div v-if="result" class="result_box">
          <div class="result_box__title">گروه احساسی تشخیص داده شده:</div>
          <div>{{ result.final }}</div>
        </div>
        <div class="container table_box" v-if="result">
          <div class="table ">
            <div>
              <a class="table_title">خشمگین</a>
              <a class="table_text">{{ result.Furious }}</a>
            </div>
            <div>
              <a class="table_title">عصبانی</a>
              <a class="table_text">{{ result.Angry }}</a>
            </div>
            <div>
              <a class="table_title">خنثی</a>
              <a class="table_text">{{ result.Neutral }}</a>
            </div>
            <div>
              <a class="table_title">خوشحال</a>
              <a class="table_text">{{ result.Happy }}</a>
            </div>
            <div>
              <a class="table_title">بسیار راضی</a>
              <a class="table_text">{{ result.Delighted }}</a>
            </div>
          </div>
        </div>
        <!--        <span> {{ result }} </span>-->
      </div>
      <div class="container flex-1 my_radio my_radio_2">
        <div>مقدار جامعه هدف</div>
        <div>
          <input type="radio" v-model="percentage" id="p10" value="10"/>
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
          break
        case -2 :
          this.result['final'] = 'خشمگین'
          break
        case -1 :
          this.result['final'] = 'عصبانی'
          break
        case 1 :
          this.result['final'] = 'خوشحال'
          break
        case 2 :
          this.result['final'] = 'بسیار راضی'
          break
      }

    }
  }
};
</script>

<style lang="scss" scoped>
$primary: #e8ffff;
$primary2: #a6f6f1;
$primary3: #41aea9;
$primary4: #213e3b;

.flex-1 {
  flex: 1;
}

.my_main {
  width: 100%;
  background-color: $primary2;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  height: 100vh;
}

.my_main_2 {
  display: flex;
  width: 80%;
}

.my_radio {
  display: inline-flex;
  color: $primary4;
  flex-direction: column;
  height: 100%;
  font-weight: 500;
}

.my_radio div {
  margin: 4px;
}

.my_radio_2 div {
  direction: rtl;
  margin-left: 12px;
  text-align: right;
}

.comment_box {
  display: flex;
  flex-direction: column;
  flex: 2;
  direction: rtl;
}

#comment_text {
  width: 100%;
  font-family: Samim;
  resize: none;
  background-color: $primary;
  box-shadow: 0 0 20px 0 rgba(0, 0, 0, 0.1), 0 5px 5px 0 rgba(0, 0, 0, 0.15);
  border: none;
  outline: none;
  color: $primary4;
  padding: 20px;
  line-height: 20px;
  font-size: 16px;
  border-radius: 5px;
}

#submit_btn {
  margin-top: 16px;
  padding: 8px;
  width: 100px;
  text-align: center;
  border-radius: 5px;
  box-shadow: 0 0 20px 0 rgba(0, 0, 0, 0.1), 0 5px 5px 0 rgba(0, 0, 0, 0.15);
  color: white;
  background-color: $primary3;
  font-size: 14px;
  cursor: pointer;
  align-self: center;
  transition: all 0.3s ease;

  &:hover {
    background: darken($primary3, 5);
    border-color: darken($primary3, 10);
  }
}

.table_box {
  margin-top: 24px;
  width: 100%;
  display: inline-block;
}

.table {
  direction: rtl;
  display: flex;
  width: 100%;
  border-radius: 5px;
  overflow: hidden;
  box-shadow: 0 0 20px 0 rgba(0, 0, 0, 0.1), 0 5px 5px 0 rgba(0, 0, 0, 0.15);
}

.table div {
  display: flex;
  flex-direction: column;
  width: 20%;
  text-align: center;
  direction: ltr;
}

.table_title {
  padding: 10px 0;
  color: white;
  background-color: $primary3;
  border-bottom: 1px solid $primary4;
}

.table_text {
  padding: 8px 0;
  background-color: $primary;
}

.result_box {
  width: 100%;
  margin: 16px 0;
  text-align: right;
  display: flex;
  align-items: center;

  &__title {
    font-size: 18px;
    font-weight: 500;
    margin-left: 5px;
  }
}
</style>
