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

import {succeddedPayment, uncapturedPayment, refundedPayment } from './PaymentData.js'
export default {
  data() {
    return {
      paymentDatabase: [],
      activeTab: 'succedded',
    }
  },
  computed: {
    getPaymentDetails() {
      if (this.activeTab === 'all') {
        this.paymentDatabase = succeddedPayment
          .concat(refundedPayment)
          .concat(uncapturedPayment)
      } else if (this.activeTab === 'succedded') {
        this.paymentDatabase = succeddedPayment
      } else if (this.activeTab === 'refunded') {
        this.paymentDatabase = refundedPayment
      } else {
        this.paymentDatabase = uncapturedPayment
      }

      return this.paymentDatabase
    },
  },
  methods: {
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
    padding: 15px 5px;

    margin-right: 5px;
  }

  .tab1 {
    min-width: 4%;
  }
  .tab2 {
    min-width: 9%;
  }
  .tab3 {
    min-width: 10%;
  }
  .tab4 {
    min-width: 44%;
  }
  .tab5 {
    min-width: 14%;
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
.selection-tab {
  .tab1,
  .tab2,
  .tab3,
  .tab4 {
    cursor: pointer;
  }
}
.succedded,
.refunded,
.uncaptured {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  padding: 2px 6px 2px 6px;
  border-radius: 26px;
  font-family: 'Times New Roman', Times, serif !important;


  img {
    height: 70%;
    width: 70%;
    margin-left: 5px;
  }
}

.succedded {
  background: #cbf4c9;
  color: #0e6245;
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
