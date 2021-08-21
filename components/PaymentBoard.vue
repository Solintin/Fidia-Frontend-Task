<template>
  <div>
    <div class="selection-tab">
      <div
        :class="[activeTab === 'all' ? 'active' : null, 'tab1']"
        @click="switchToAll"
      >
        All
      </div>
      <div
        :class="[activeTab === 'succedded' ? 'active' : null, 'tab2']"
        @click="switchToSuccedded"
      >
        Succedded
      </div>
      <div
        :class="[activeTab === 'refunded' ? 'active' : null, 'tab3']"
        @click="switchToRefunded"
      >
        Refunded
      </div>
      <div
        :class="[activeTab === 'uncaptured' ? 'active' : null, 'tab4']"
        @click="switchToUncaptured"
      >
        uncaptured
      </div>
      <div class="tab5"></div>
      <div class="tab6"></div>
    </div>

    <div class="payment-board-tabs">
      <div class="tab1"><input type="checkbox" checked /></div>
      <div class="tab2">Amount</div>
      <div class="tab3"></div>
      <div class="tab4">Description</div>
      <div class="tab5">Customer</div>
      <div class="tab6">Date</div>
    </div>

    <div
      class="payment-board"
      v-for="(payment, id) in getPaymentDetails"
      :key="id"
    >
      <div class="tab1"><input type="checkbox" /></div>
      <div class="tab2">
        <span>US$ {{ payment.amount }}</span>
      </div>
      <div class="tab3">
        <span :class="payment.state">
          <span>{{ payment.state }}</span>
          <span>
            <img :src="require(`@/assets/icons/${payment.icon}`)" alt="" />
          </span>
        </span>
      </div>
      <div class="tab4">
        <span> {{ payment.desc }} </span>
      </div>
      <div class="tab5">
        <span> {{ payment.customer }} </span>
      </div>
      <div class="tab6">
        <span> {{ payment.date }} </span>
      </div>
      <div class="tab7"><span> ... </span></div>
    </div>
  </div>
</template>

<script>
import RefundedPaymentData from '~/Data/RefundedPaymentData.js' //importing Refundedpayment Details JSON Endpoint
import SucceddedPaymentData from '~/Data/SucceddedPaymentData.js' //importing Suceddedpayment Details JSON Endpoint
import UncapturedPaymentData from '~/Data/UncapturedPaymentData.js' //importing Uncaptueredpayment Details JSON Endpoint
export default {
  data() {
    return {
      paymentDatabase: [],
      activeTab: 'succedded',
    }
  },
  computed: {
    // Dynamic Data(All, Sucedded, Refunded And Uncaptured) Rendering On the Dashboard
    getPaymentDetails() {
      if (this.activeTab === 'all') {
        this.paymentDatabase = SucceddedPaymentData.concat(
          RefundedPaymentData
        ).concat(UncapturedPaymentData)
      } else if (this.activeTab === 'succedded') {
        this.paymentDatabase = SucceddedPaymentData
      } else if (this.activeTab === 'refunded') {
        this.paymentDatabase = RefundedPaymentData
      } else {
        this.paymentDatabase = UncapturedPaymentData
      }

      return this.paymentDatabase
    },
  },
  methods: {
    // Functions To Switch Tabs

    switchToAll() {
      this.activeTab = 'all'
      this.getPaymentDetails
    },
    switchToSuccedded() {
      this.activeTab = 'succedded'
      this.getPaymentDetails
    },
    switchToRefunded() {
      this.activeTab = 'refunded'
      this.getPaymentDetails
    },
    switchToUncaptured() {
      this.activeTab = 'uncaptured'
      this.getPaymentDetails
    },
  },
}
</script>

<style lang="scss" scoped>
.selection-tab,
.payment-board-tabs,
.payment-board {
  display: flex;
  align-items: center;
  flex-direction: row;
  flex-wrap: nowrap;
  margin-top: 5px;
  border-bottom: 1px solid #e3e8ee;
  font-size: 14px;

  div {
    padding: 10px 5px;

    margin-right: 5px;
  }

  .tab1 {
    min-width: 3%;
  }
  .tab2 {
    min-width: 9%;
    display: flex;
    // justify-content: center;
   
  }
  .tab3 {
    min-width: 10%;
    display: flex;
    justify-content: center;
  }
  .tab4 {
    min-width: 44%;
  }
  .tab5 {
    min-width: 15%;
  }
  .tab6 {
    min-width: 14%;
    margin-left: 10px;
  }
  .tab7 {
    min-width: 4%;
  }
  .active {
    border-bottom: 2px solid #7a73ff;
    color: #7a73ff;
    margin-bottom: -1px;
  }
}
input[type='checkbox'] {
  // background: #ffffff;
  outline: none;
  // border : none;
  box-shadow: 0px 2px 5px rgba(60, 66, 87, 0.08),
    0px 0px 0px 1px rgba(60, 66, 87, 0.16), 0px 1px 1px rgba(0, 0, 0, 0.12);
  border-radius: 4px;
}
.selection-tab {
  .tab1,
  .tab2,
  .tab3,
  .tab4 {
    font-weight: 500;
    cursor: pointer;
    font-style: normal;
    font-size: 14px;
    line-height: 16.71px; 
  }
}
.succedded,
.refunded,
.uncaptured {
 display: flex;
flex-direction: row;
align-items: center;
padding: 1px 4px 1px 6px;
  font-weight : 600;
  border-radius: 4px;
font-style: normal;
font-size: 12px;
line-height: 14px;
  img {
    height: 10px;
    width: 10px;
    margin-left: 5px;
  }
}
.payment-board-tabs{
  text-transform: uppercase;
  font-size: 12px;
}
.payment-board {
  color: #4F566B;
  font-style: normal;
font-weight: normal;
font-size: 13px;
line-height: 16px;
.tab2{
font-style: normal;
color: #1A1F36;
font-weight: 600;
font-size: 14px;
line-height: 17px;
text-align: right !important;
}
}
.succedded {
  background: #cbf4c9;
  font-style: normal;
font-weight: 500;
font-size: 12px;
line-height: 14px;
display: flex;
align-items: center;

/* Dark green */

color: #0E6245;
}
.refunded {
  background: #3374b1d5;
  color: #07345ed5;
}
.uncaptured {
  background: #be515a;
  color: #e0c0c3;
}
</style>
