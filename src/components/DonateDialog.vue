<template>
  <dialog-modal title="Support">
    <div class="donate-container">
      <div class="dialog-container">
        <div class="donate-sub-container">
          <div>
            <div>
              {{ campaign.percentage_rasied }}%
              <span>
                <svg
                  class="dayleft-logo"
                  viewBox="0 0 7 6"
                  fill="none"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    fill-rule="evenodd"
                    clip-rule="evenodd"
                    d="M0.561387 2.91122C0.561387 1.34492 1.83563 0.0706787 3.40193 0.0706787C4.96824 0.0706787 6.24247 1.34492 6.24247 2.91122C6.24247 4.47752 4.96824 5.75176 3.40193 5.75176C1.83563 5.75176 0.561387 4.47753 0.561387 2.91122ZM1.18231 2.91125C1.18231 4.1352 2.17802 5.13091 3.40197 5.13091C4.62592 5.13091 5.62162 4.1352 5.62162 2.91125C5.62162 1.68736 4.62592 0.691597 3.40197 0.691597C2.17802 0.691597 1.18231 1.68736 1.18231 2.91125Z"
                    fill="currentColor"
                  />
                  <path
                    d="M3.64778 2.91458V1.72405C3.64778 1.59112 3.54005 1.4834 3.40717 1.4834C3.27425 1.4834 3.16652 1.59112 3.16652 1.72405V2.99146C3.16652 2.99525 3.16745 2.9988 3.16764 3.00258C3.16447 3.06802 3.18701 3.13446 3.23699 3.18445L4.13324 4.08063C4.22725 4.17463 4.37961 4.17463 4.47354 4.08063C4.56748 3.98662 4.56755 3.83426 4.47354 3.74032L3.64778 2.91458Z"
                    fill="currentColor"
                  />
                </svg>
                {{ dayLeft }} days left</span
              >
            </div>
          </div>
          <div>{{ amounts }}</div>
        </div>
        <div class="healthbar">
          <div class="healthbar_value"></div>
        </div>
      </div>
    </div>
    <form @submit.prevent="submit">
      <div>
        <span>Donation amount</span>
      </div>
      <div>
        <input
          type="range"
          min="1000"
          max="5000000"
          step="100"
          class="form-input"
        />
      </div>
      <div class="form-range">
        <span>#1k</span>
        <span>#5,000,000</span>
      </div>
      <div>
        <div>
          <input
            type="number"
            ref="formAmount"
            class="input-amount"
            id="amount"
            v-model="formAmount"
            placeholder="Or enter specific amount "
            @blur="validateInput"
          />
        </div>
      </div>
      <p v-if="formAmountValidity === 'invalid'" class="error_alert">
        The entered amount must be greater than #5,000,000
      </p>
      <div>
        <h4>Tip our services</h4>
        <p>
          Fundfrica has 0% platform fee for all fundraiser orgainisers. Tipping
          keeps Fundfrica services running, all thanks to our donors.
        </p>

        <div>
          <select name="tipAmount" id="tip-percentage" v-model="tipAmount">
            <option value="fiften" selected>15%(#{{ fiftenPercent }})</option>
            <option value="ten">10%(#{{ tenPercent }})</option>
            <option value="five">5%(#{{ fivePercent }})</option>
          </select>
        </div>
      </div>
      <div>
        <button
          type="button"
          class="btn-continue"
          @click="togglePersonalDetails"
          :disabled="clickable"
        >
          {{ showPersonalDetails ? "Show Less" : "Continue" }}
        </button>
      </div>
      <div v-if="showPersonalDetails">
        <div class="form-continue">
          <div>
            <input
              type="name"
              id="first_name"
              class="form-continue-content"
              placeholder="First name"
            />
          </div>
          <div>
            <input
              type="name"
              id="second_name"
              class="form-continue-content"
              placeholder="Second name"
            />
          </div>
        </div>
        <div class="form-continue">
          <div>
            <input
              type="number"
              id="first_name"
              class="form-continue-content"
              placeholder="Phone number"
            />
          </div>
          <div>
            <input
              type="email"
              id="second_name"
              class="form-continue-content"
              placeholder="Email"
            />
          </div>
        </div>

        <button
          type="button"
          class="btn-continue"
          id="btn-continue"
          @click="toggleRecurringDetails"
          :disabled="cnt > 1"
        >
          Make a pledge
        </button>
        <pledge-alert v-if="showRecurringDetails">
          <svg
            class="btn-cancel"
            viewBox="0 0 14 16"
            fill="currentColor"
            xmlns="http://www.w3.org/2000/svg"
            @click="confirmedCancel"
          >
            <path
              d="M2.12372 15.2561C1.77439 15.2561 1.48795 15.1652 1.26438 14.9836C1.04082 14.788 0.908074 14.5504 0.866155 14.271C0.838209 13.9775 0.936019 13.6841 1.15959 13.3907L5.51913 7.56397L1.39014 2.03071C1.16657 1.7233 1.06876 1.42987 1.09671 1.15041C1.12465 0.856983 1.25041 0.619443 1.47398 0.437796C1.69754 0.242175 1.977 0.144365 2.31235 0.144365C2.82935 0.144365 3.29744 0.430809 3.71663 1.0037L7.04916 5.61475L10.3817 1.0037C10.8009 0.430809 11.276 0.144365 11.8069 0.144365C12.1563 0.144365 12.4427 0.235189 12.6663 0.416837C12.8898 0.598484 13.0156 0.836024 13.0435 1.12946C13.0715 1.40891 12.9667 1.70933 12.7291 2.03071L8.60015 7.56397L12.9387 13.3907C13.1623 13.6841 13.2601 13.9775 13.2322 14.271C13.2042 14.5504 13.0785 14.788 12.8549 14.9836C12.6313 15.1652 12.3379 15.2561 11.9746 15.2561C11.4716 15.2561 11.0035 14.9626 10.5703 14.3758L7.04916 9.55511L3.54895 14.3758C3.11579 14.9626 2.64071 15.2561 2.12372 15.2561Z"
            />
          </svg>

          <h2>Pledge a support</h2>
          <p>
            Are you sure you want to make a pledge? If a campaign is marked to
            be able to pledge support, a donor must be able to pledge an amount
            as support with the frequency of collections
          </p>
          <div class="btn-pledge">
            <button type="submit" class="btn-continue" @click="confirmedOkay">
              Recurring
            </button>
          </div>
        </pledge-alert>
        <div v-if="confirmedPledge">
          <div>
            <label for="frequency">Frequency:</label>
            <select name="referrer" id="recurring-plan" v-model="referrer">
              <option value="Monthly" selected>Monthly</option>
              <option value="Weekly">Weekly</option>
              <option value="Dialy">Dialy</option>
            </select>
          </div>
          <div>
            <label for="amount">Amount</label>
            <input
              type="number"
              name=""
              id=""
              v-model="recurringAmount"
              class="input-amount"
            />
          </div>
          <div>
            <label for="number-times">Number times</label>
            <input
              type="number"
              name=""
              id=""
              class="input-amount"
              :disabled="disableNumber"
            />
          </div>
          <div>
            <input
              type="checkbox"
              class="checkbox"
              v-model="checkbox"
              @blur="validateAmount"
            />
            <label for="never-end">Never End</label>
          </div>
        </div>
        <div>
          <button type="submit" class="btn-submit">
            Donate amount #{{ outputAmount }}
          </button>
        </div>
      </div>
    </form>
    <!-- <keep-alive>
      <component :is="component" />
    </keep-alive> -->
  </dialog-modal>
</template>
<script>
import DialogModal from "./DialogModal.vue";
import PledgeAlert from "./PledgeAlert.vue";

export default {
  components: {
    "dialog-modal": DialogModal,
    "pledge-alert": PledgeAlert,
  },

  data() {
    return {
      campaign: {
        amount: "#100,000",
        days_left: 0,
        percentage_rasied: 0,
      },
      formAmount: "",
      showPersonalDetails: false,
      showRecurringDetails: false,
      confirmedPledge: false,
      isActive: true,
      tipAmount: "fiften",
      referrer: "",
      outputAmount: 0,
      amountToDonate: 0,
      formAmountValidity: "pending",
      checkbox: "",
      recurringAmount: "",
      disableNumberInput: "pending",
      cnt: 1,
    };
  },
  watch: {
    amount: {
      handler() {
        this.formAmount = this.recurringAmount;
      },
    },
    amountToDonate: {
      handler() {
        if (this.tipAmount === "fiften") {
          const tip15 = this.formAmount + this.fiftenPercent;
          return (this.outputAmount = tip15);
        }
      },
    },
    recurringPayment: {
      handler() {
        if (this.referrer !== "Monthly") {
          if (new Date() === this.next30Days) {
            this.submit;
          }
        }
      },
    },
  },
  computed: {
    disableNumber() {
      return this.disableNumberInput === "invalid";
    },
    clickable() {
      return this.formAmountValidity === "invalid";
    },

    next30Days() {
      Date.prototype.addDays = function (days) {
        var date = new Date(this.valueOf());
        date.setDate(date.getDate() + days);
        return date;
      };
      var date = new Date();
      return date.addDays(30);
    },
    next7Days() {
      Date.prototype.addDays = function (days) {
        var date = new Date(this.valueOf());
        date.setDate(date.getDate() + days);
        return date;
      };
      var date = new Date();
      return date.addDays(7);
    },
    nextDay() {
      Date.prototype.addDays = function (days) {
        var date = new Date(this.valueOf());
        date.setDate(date.getDate() + days);
        return date;
      };
      var date = new Date();
      return date.addDays(1);
    },
    amounts() {
      return this.campaign.amount.toString();
    },
    dayLeft() {
      const oneDay = 24 * 60 * 60 * 1000;
      const firstDate = new Date(2022, 7, 5);
      const secondDate = new Date();
      const diffDate = Math.round(Math.abs(firstDate - secondDate) / oneDay);
      return diffDate;
    },
    fiftenPercent() {
      const fiften = this.formAmount * 0.15;
      return fiften;
    },
    tenPercent() {
      const fiften = this.formAmount * 0.1;
      return fiften;
    },
    fivePercent() {
      const fiften = this.formAmount * 0.05;
      return fiften;
    },
  },
  methods: {
    validateAmount() {
      if (this.checkbox === true) {
        this.disableNumberInput = "invalid";
      } else {
        this.disableNumberInput = "valid";
      }
    },
    validateInput() {
      if (this.formAmount > 5000000) {
        this.formAmountValidity = "invalid";
      } else {
        this.formAmountValidity = "valid";
      }
    },
    submit() {
      if (this.formAmount === "") console.log("success");
      console.log("checkbox:", this.checkbox);
      console.log(this.recurringAmount);
      if (this.checkbox === true) {
        console.log("hello");
      }
    },

    togglePersonalDetails() {
      this.showPersonalDetails = !this.showPersonalDetails;
    },
    toggleRecurringDetails() {
      // this.showRecurringDetails = true;
      if (!this.showRecurringDetails) {
        this.showRecurringDetails = true;
        // something to do
        this.cnt = ++this.cnt;
      }
    },
    confirmedOkay() {
      this.confirmedPledge = true;
      this.showRecurringDetails = false;
    },
    confirmedCancel() {
      this.showRecurringDetails = false;
    },
  },
};
</script>

<style scoped>
.btn-cancel {
  width: 20px;
  position: absolute;
  padding-right: 10px;
  right: 0;
  margin: auto;
}
.dayleft-logo {
  width: 17px;
}
.error_alert {
  color: red;
  font-size: 15px;
}
.btn-pledge {
  display: flex;
  justify-content: space-between;
  margin: 0, auto;
}
#btn-continue {
  margin-top: 1rem;
  width: 100%;
  margin: 0, auto;
}
.btn-submit {
  text-align: center;
  color: white;
  font-size: 25px;
  width: 100%;
  margin: 0, auto;
  padding: 15px;
  font-weight: 400;
  background-color: rgb(56, 183, 56);
  border: 1px solid rgb(56, 183, 56);
  border-radius: 00.5rem;
  margin-top: 2rem;
  margin-bottom: 10px;
}
.form-continue-content {
  width: 100%;
  padding: 10px;
  border-radius: 0.5rem;
  border: 1px solid #534b4b6b;
}
.form-continue {
  display: flex;
  justify-content: space-between;
  width: 100%;

  margin: 0, auto;
}
.button {
  display: flex;
  justify-content: space-between;
}
.btn-continue {
  padding: 10px;
  background-color: #008cff;
  border: none;
  border-radius: 0.5rem;
  color: white;
  font-size: 16px;
}
#tip-percentage,
#recurring-plan {
  border: none;
  font-size: 17px;
  border-bottom: 2px solid #534b4b6b;
  color: #534b4b6b;
  width: 100%;
  margin: 0, auto;
  padding-bottom: 10px;
}
form div {
  margin-top: 1rem;
}
.input-amount {
  margin: 0, auto;
  border-radius: 0.5rem;
  padding: 10px;
  border: 1px solid #534b4b6b;
}
input {
  width: 100%;
  margin: 0, auto;
  margin-top: 1rem;
}
input[type="checkbox"] {
  padding: 0;
  width: 20px;
}
.form-range {
  margin-top: 0.5rem;
  display: flex;
  justify-content: space-between;
  margin: 0, auto;
}
.dialog-container {
  padding: 15px;
}
.donate-container {
  margin-top: 1rem;
  margin: 0, auto;

  border: 1 px solid rgba(124, 189, 215, 0.279);
  border-top-left-radius: 1.5rem;
  border-top-right-radius: 1.5rem;
  border-bottom-left-radius: 2px;
  border-bottom-right-radius: 2px;
  background-color: rgba(124, 189, 215, 0.279);
}
.donate-sub-container {
  display: flex;
  justify-content: space-between;
  margin: 0, auto;
}
.healthbar {
  width: 100%;
  height: 10px;
  border: 1px solid #e1dcdc;
  border-radius: 2rem;
  /* margin: 2rem 0; */
  margin-top: 1rem;
  background: #e1dcdc;
  margin-right: 20px;
}

.healthbar__value {
  background-color: #00a876;
  width: 100%;
  height: 100%;
}
</style>
