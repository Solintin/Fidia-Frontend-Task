<template>
  <div>
    <div class="selection-tab">
      <div class="tab1" @click="switchToAll">
        <span :class="[activeTab === 'all' ? 'active' : null, 'pb-2']">
          All</span
        >
      </div>
      <div class="tab2 d-flex justify-content-center" @click="switchToSuccedded">
        <span :class="[activeTab === 'succedded' ? 'active' : null, 'pb-2']">
          Succedded</span
        >
      </div>
      <div class="tab3" @click="switchToRefunded">
        <span :class="[activeTab === 'refunded' ? 'active' : null, 'pb-2']">
          Refunded</span
        >
      </div>
      <div class="tab4" @click="switchToUncaptured">
        <span :class="[activeTab === 'uncaptured' ? 'active' : null, 'pb-2']">
          Uncaptured</span
        >
      </div>
      <div class="tab5 pb-2"></div>
      <div class="tab6 pb-2"></div>
    </div>

    <div class="payment-board-tabs text-uppercase py-2">
      <div class="tab1"><input type="checkbox" checked /></div>
      <div class="tab2 text-center">Amount</div>
      <div class="tab3"></div>
      <div class="tab4">Description</div>
      <div class="tab5">Customer</div>
      <div class="tab6">Date</div>
    </div>

    <div
      class="payment-board py-1"
      v-for="(payment, id) in getPaymentDetails"
      :key="id"
    >
      <div class="tab1 py-1"><input type="checkbox" /></div>
      <div class="tab2 text-end fs-6">
        <span>US$ {{ payment.amount }}</span>
      </div>
      <div class="tab3 text-capitalize">
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
.payment-board-tabs {
  font-size: 12px;
}
.selection-tab,
.payment-board-tabs,
.payment-board {
  display: flex;
  align-items: center;
  flex-direction: row;
  flex-wrap: nowrap;
  margin-top: 5px;
  border-bottom: 1px solid #e3e8ee;

  .tab1 {
    min-width: 4%;
    display: flex;
  }
  .tab2 {
    min-width: 9%;
  }
  .tab3 {
    min-width: 10%;
    display: flex;
    justify-content: center;
    margin: 0 10px 0 8px;
  }
  .tab4 {
    min-width: 42%;
    display: flex;
  }
  .tab5 {
    min-width: 15%;
  }
  .tab6 {
    min-width: 14%;
    margin-left: 10px;
  }
  .tab7 {
    min-width: 5%;
    display: flex;
    align-items: center;
  }
  .active {
    border-bottom: 2px solid #7a73ff;
    color: #7a73ff;
    margin-bottom: -1px;
    width: min-content;
  }
}
input[type='checkbox'] {
  box-shadow: 0px 0px 10px rgba(10, 28, 94, 0.12);
  border-radius: 10px;
  transform: scale(1.15);
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
  padding: 3px 4px 4px 6px;
  font-weight: 600;
  border-radius: 4px;
  font-style: normal;
  font-size: 12px;
  line-height: 14px;
  img {
    height: 13px;
    width: 13px;
    margin-left: 5px;
  }
}

.payment-board {
  color: #4f566b;
  font-style: normal;
  font-weight: normal;
  font-size: 13px;
  line-height: 16px;
  .tab2 {
    font-style: normal;
    color: #1a1f36;
    font-weight: 600;
    font-size: 14px;
    line-height: 17px;
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

  color: #0e6245;
}
.refunded {
  background: #3374b1d5;
  color: #07345ed5;
}
.uncaptured {
  background: #e7717b;
  color: #f7f7f7;
}
</style>
