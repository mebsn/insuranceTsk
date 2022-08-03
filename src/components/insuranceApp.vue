<template>
  <div class="insuranceContainer">
    <article class="insuranceContent">
      <h1>Quam Tristique Condimentum</h1>
      <p>
        Duis mollis, est non commodo luctus, nisi erat porttitor ligula, eget
        lacinia odio sem nec elit. Cum sociis natoque penatibus et magnis dis
        parturient montes, nascetur ridiculus mus. <a> Curabitur blandit </a>
        tempus porttitor. Integer posuere erat a ante venenatis dapibus posuere
        velit aliquet. Vestibulum id ligula porta felis euismod semper.
      </p>
      <section>
        <div class="additionalInfo">
          <h2>Fringilla Euismod Adipiscing Ipsum</h2>
          <p>
            Cum sociis natoque penatibus et magnis dis parturient montes,
            nascetur ridiculus mus. Maecenas faucibus mollis interdum. Aenean
            lacinia bibendum nulla sed.
          </p>
          <div class="additionalInfo_list">
            <div class="additionalInfo_list-item">
              <div class="redLine"></div>
              <p>Tellus Ullamcorper Inceptos</p>
            </div>
            <div class="additionalInfo_list-item">
              <div class="redLine"></div>
              <p>Magna Condimentum</p>
            </div>
            <div class="additionalInfo_list-item">
              <div class="greenLine"></div>
              <p>Mattis Tristique</p>
            </div>
            <div class="additionalInfo_list-item">
              <div class="greenLine"></div>
              <p>Pharetra Pellentesque Dapibus</p>
            </div>
            <div class="additionalInfo_list-item">
              <div class="redLine"></div>
              <p>Aenean Inceptos</p>
            </div>
            <div class="additionalInfo_list-item">
              <div class="redLine"></div>
              <p>Parturient Bibendum</p>
            </div>
          </div>
        </div>
        <img src="../assets/Image.png" />
      </section>
    </article>
    <div class="insuranceCalculator">
      <h4>Compensation Calculator</h4>
      <label>Average income</label>
      <input type="number" v-model="income" />
      <span class="euroSign">€</span>
      <label>Days on sick-leave</label>
      <input type="number" v-model="days" />
      <span class="daysQuantity">Days</span>
      <div class="checkboxDiv">
        <input class="checkbox" type="checkbox" @click="checkTuberculosis()" />
        <span class="tubercolosis">I have tubercolosis</span>
      </div>
      <div class="calculate" @click="calculation()">Calculate</div>
      <div class="validation" v-if="validation">You must fill both fields!</div>
      <div class="calculationResults">
        <div class="employerCalc">
          <h6>The employer compensates</h6>
          <div class="employerDaysQuantity">{{ employerDays }} days</div>
          <div class="employerTotalCompensation">{{ totalEmployerPay }} €</div>
          <span class="daily">daily allowance</span>
          <div class="dailyCompensation">{{ dailyIncome }} €</div>
        </div>
        <div class="companyCalc">
          <h6>Health insurance compensates</h6>
          <div class="companyDaysQuantity">{{ companyDays }} days</div>
          <div class="companyTotalCompensation">{{ totalCompanyPay }} €</div>
          <span class="daily">daily allowance</span>
          <div class="dailyCompensation">{{ dailyIncome }} €</div>
        </div>
      </div>
      <div class="finalresultText">
        Compensation total for {{ days }} days (net)
      </div>
      <div class="finalResult">{{ totalPay }} €</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "insuranceApp",
  data() {
    return {
      days: null,
      income: null,
      dailyIncome: null,
      employerDays: null,
      companyDays: null,
      totalEmployerPay: null,
      totalCompanyPay: null,
      totalPay: null,
      validation: false,
      tuberculosisChecked: false,
    };
  },
  methods: {
    checkTuberculosis() {
      this.tuberculosisChecked = !this.tuberculosisChecked;
    },
    calculation() {
      if (this.days == null || this.income == null) {
        this.validation = true;
        let self = this;
        setTimeout(function () {
          self.validation = false;
        }, 3000);
      } else {
        this.dailyIncome = Math.floor(((this.income / 30) * 70) / 100);
        if (this.days > 3 && this.days < 9) {
          this.employerDays = this.days - 3;
          this.totalEmployerPay = this.dailyIncome * this.employerDays;
        } else if (this.days < 4) {
          this.employerDays = 0;
          this.totalEmployerPay = this.dailyIncome * this.employerDays;
        } else if (this.days > 8) {
          this.employerDays = 5;
          this.totalEmployerPay = this.dailyIncome * this.employerDays;
        }
      }
      if (this.tuberculosisChecked == false) {
        if (this.days > 8 && this.days < 183) {
          this.companyDays = this.days - 8;
          this.totalCompanyPay = this.companyDays * this.dailyIncome;
        } else if (this.days < 9) {
          this.companyDays = 0;
          this.totalCompanyPay = this.companyDays * this.dailyIncome;
        } else if (this.days > 182) {
          this.companyDays = 182 - 8;
          this.totalCompanyPay = this.companyDays * this.dailyIncome;
        }
      } else if (this.tuberculosisChecked == true) {
        if (this.days > 8 && this.days < 241) {
          this.companyDays = this.days - 8;
          this.totalCompanyPay = this.companyDays * this.dailyIncome;
        } else if (this.days < 9) {
          this.companyDays = 0;
          this.totalCompanyPay = this.companyDays * this.dailyIncome;
        } else if (this.days > 240) {
          this.companyDays = 240 - 8;
          this.totalCompanyPay = this.companyDays * this.dailyIncome;
        }
      }
      this.totalPay = this.totalCompanyPay + this.totalEmployerPay;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Sora");
.validation {
  width: 100%;
  height: 20px;
  font-family: "sora";
  font-style: normal;
  font-weight: 700;
  font-size: 14px;
  line-height: 15px;
  color: #e1261c;
  margin-top: 15px;
  text-align: center;
}
.insuranceContainer {
  width: 1280px;
  display: flex;
  justify-content: space-between;
  flex-direction: row;
}
a {
  color: #e1261c;
  text-decoration: underline;
}
.insuranceContent {
  width: 660px;
  height: 100%;
  display: flex;
  flex-direction: column;
  margin-top: 100px;
  margin-left: 100px;
  margin-bottom: 100px;
}
h1 {
  font-family: "Sora";
  font-style: normal;
  font-weight: 700;
  font-size: 40px;
  letter-spacing: -0.02em;
  color: #ffffff;
}
h2 {
  font-family: "Sora";
  font-style: normal;
  font-weight: 700;
  font-size: 32px;
  line-height: 35px;
  letter-spacing: -0.02em;
  color: #ffffff;
}
p {
  font-family: "Sora";
  font-style: normal;
  font-weight: 300;
  font-size: 18px;
  line-height: 30px;
  color: #ffffff;
}
section {
  width: 660px;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}
.additionalInfo {
  width: 380px;
}
.additionalInfo_list {
  width: 380px;
}
img {
  width: 240px;
  height: 180px;
  margin-top: 30px;
}
.redLine {
  width: 16px;
  height: 4px;
  background: linear-gradient(90deg, #911812 0%, #e1261c 100%);
  margin-left: 5px;
}
.greenLine {
  width: 12px;
  height: 4px;
  margin-left: 34px;
  background: linear-gradient(90deg, #d3dae8 0%, #a7b7d8 100%);
}
.additionalInfo_list-item {
  display: flex;
  flex-direction: row;
  align-items: center;
  height: 35px;
  margin-top: 5px;
}
.additionalInfo_list-item p {
  margin-left: 9px;
}
.insuranceCalculator {
  width: 320px;
  height: 755px;
  background-color: #ffffff;
  margin-top: 140px;
  margin-right: 100px;
  position: relative;
  display: flex;
  align-items: center;
  flex-direction: column;
}
.insuranceCalculator:before,
.insuranceCalculator:after {
  content: "";
  position: absolute;
  left: 0;
  right: 0;
  bottom: 100%;
  border-bottom: 15px solid white;
  border-left: 15px solid transparent;
  border-right: 15px solid transparent;
  top: -14px;
}
.insuranceCalculator:after {
  bottom: auto;
  top: 99.9%;
  border-bottom: none;
  border-top: 20px solid white;
}
h4 {
  margin-top: 80px;
  width: 280px;
  height: 50px;
  font-family: "Sora";
  font-style: normal;
  font-weight: 700;
  font-size: 24px;
  line-height: 25px;
  letter-spacing: -0.02em;
  color: #111317;
  margin-bottom: 10px;
}
label {
  height: 20px;
  width: 280px;
  font-family: "sora";
  font-style: normal;
  font-weight: 600;
  font-size: 14px;
  line-height: 20px;
  color: #111317;
  margin-top: 20px;
}
input {
  width: 270px;
  height: 50px;
  margin-top: 5px;
  background: #ffffff;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  color: #111317;
  border: 2px solid grey;
  font-family: "sora";
  font-style: normal;
  font-weight: 400;
  padding-left: 10px;
  font-size: 18px;
  line-height: 30px;
  color: #111317;
  position: relative;
}
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}
input[type="number"] {
  -moz-appearance: textfield;
}
.euroSign {
  position: absolute;
  top: 198px;
  right: 40px;
  z-index: 10;
  font-family: "sora";
  font-style: normal;
  font-weight: 700;
  font-size: 18px;
  line-height: 30px;
  text-align: right;
  color: #111317;
}
.daysQuantity {
  position: absolute;
  z-index: 10;
  top: 298px;
  right: 40px;
  font-family: "sora";
  font-style: normal;
  font-weight: 700;
  font-size: 18px;
  line-height: 30px;
  text-align: right;
  color: #111317;
}
.checkboxDiv {
  width: 280px;
  height: 20px;
  display: flex;
  flex-direction: row;
  margin-top: 20px;
  align-items: center;
}
input[type="checkbox"] {
  width: 20px;
  height: 20px;
}
input[type="checkbox"]:checked {
  width: 20px;
  height: 20px;
  background-color: black !important;
}
.tubercolosis {
  font-family: "sora";
  font-style: normal;
  font-weight: 700;
  font-size: 14px;
  line-height: 30px;
  text-align: right;
  color: #111317;
  margin-left: 10px;
}
.calculate {
  margin-top: 20px;
  background: linear-gradient(90deg, #911812 0%, #e1261c 100%);
  border-radius: 30px;
  width: 169px;
  height: 60px;
  color: white;
  font-family: "sora";
  font-style: normal;
  font-weight: 700;
  font-size: 18px;
  line-height: 20px;
  color: #ffffff;
  text-shadow: 2px 2px 0px rgba(0, 0, 0, 0.4);
  display: flex;
  align-items: center;
  justify-content: center;
  margin-left: -110px;
  cursor: pointer;
}
.calculationResults {
  width: 100%;
  height: 154px;
  border-top: 2px solid #e9edf4;
  border-bottom: 2px solid #e9edf4;
  display: flex;
  flex-direction: row;
  margin-top: 20px;
}
.employerCalc {
  width: 50%;
  height: 100%;
  display: flex;
  flex-direction: column;
}
.companyCalc {
  width: 50%;
  height: 100%;
  display: flex;
  flex-direction: column;
}
h6 {
  width: 100%;
  height: 30px;
  text-align: center;
  font-family: "sora";
  font-style: normal;
  font-weight: 700;
  font-size: 16px;
  margin-top: 15px;
  color: #111317;
}
.employerDaysQuantity {
  font-family: "sora";
  font-style: normal;
  font-weight: 700;
  font-size: 16px;
  color: #111317;
  width: 100%;
  text-align: center;
  margin-top: -25px;
}
.employerTotalCompensation {
  font-family: "sora";
  font-style: normal;
  font-weight: 700;
  font-size: 18px;
  line-height: 15px;
  color: #111317;
  width: 100%;
  text-align: center;
  margin-top: 15px;
}
.companyDaysQuantity {
  font-family: "sora";
  font-style: normal;
  font-weight: 700;
  font-size: 16px;
  color: #111317;
  width: 100%;
  text-align: center;
  margin-top: -25px;
}
.companyTotalCompensation {
  font-family: "sora";
  font-style: normal;
  font-weight: 700;
  font-size: 18px;
  line-height: 15px;
  color: #111317;
  width: 100%;
  text-align: center;
  margin-top: 15px;
}
.daily {
  font-family: "sora";
  font-style: normal;
  font-weight: 700;
  font-size: 14px;
  line-height: 15px;
  color: #7a818e;
  width: 100%;
  text-align: center;
  margin-top: 5px;
}
.dailyCompensation {
  font-family: "sora";
  font-style: normal;
  font-weight: 700;
  font-size: 14px;
  line-height: 15px;
  color: #7a818e;
  margin-top: 5px;
  width: 100%;
  text-align: center;
}
.finalresultText {
  width: 100%;
  font-family: "sora";
  font-style: normal;
  font-weight: 700;
  font-size: 14px;
  line-height: 15px;
  color: #111317;
  margin-top: 10px;
  text-align: center;
}
.finalResult {
  width: 100%;
  font-family: "sora";
  font-style: normal;
  font-weight: 700;
  font-size: 24px;
  line-height: 15px;
  color: #111317;
  margin-top: 15px;
  text-align: center;
  height: 20px;
  display: flex;
  justify-content: center;
}
@media only screen and (max-width: 1280px) {
  .insuranceContainer {
    flex-direction: column;
    align-items: center;
    display: flex;
    width: 100%;
  }
  .insuranceContent {
    width: 660px;
    height: 100%;
    display: flex;
    flex-direction: column;
    margin-left: 0px;
    align-items: center;
  }
  .insuranceCalculator {
    width: 420px;
    height: 755px;
    background-color: #ffffff;
    margin-top: 0px;
    margin-left: 100px;
    margin-bottom: 100px;
  }
  .euroSign {
    right: 80px;
  }
  .daysQuantity {
    right: 80px;
  }
}
@media only screen and (max-width: 760px) {
  section {
    width: 400px;
    display: flex;
    flex-direction: column-reverse;
    justify-content: center;
    margin-top: 30px;
    align-items: center;
  }
  .additionalInfo {
    display: flex;
    align-items: center;
    flex-direction: column;
  }
  .additionalInfo_list-item {
    margin-left: 25px;
  }
  h1 {
    font-size: 32px;
    width: 240px;
    margin-bottom: 60px;
  }
  h2 {
    font-size: 20px;
    margin-top: 40px;
  }
  p {
    font-size: 18px;
  }
  .insuranceContent {
    width: 400px;
    align-items: center;
    display: flex;
  }
  img {
    width: 90%;
    height: 180px;
  }
}
@media only screen and (max-width: 480px) {
  section {
    width: 320px;
    display: flex;
    flex-direction: column-reverse;
    justify-content: center;
    margin-top: 30px;
    align-items: center;
  }
  .additionalInfo {
    display: flex;
    align-items: center;
    flex-direction: column;
    width: 320px;
  }
  .additionalInfo_list {
    width: 280px;
  }
  .additionalInfo-item {
    width: 320px;
  }
  h1 {
    font-size: 28px;
    width: 240px;
  }
  h2 {
    font-size: 18px;
  }
  p {
    font-size: 14px;
    margin-left: 4px;
  }
  .insuranceContent {
    width: 320px;
    align-items: center;
    display: flex;
  }
  .insuranceCalculator {
    width: 100%;
  }
  .calculationResults {
    height: 170px;
  }
  .euroSign {
    right: 20%;
  }
  .daysQuantity {
    right: 20%;
  }
}
</style>
