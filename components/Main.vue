<template>
  <div>
    <div class="main">

      <!-- =========== Dashbaord Header Begins ============= -->
      <header>
        <div>
          <span> <img src="@/assets/icons/search-icon.svg" /> </span>
          <!-- Dashboard SearchBar -->
          <input type="search" name="" placeholder="Search..." />
        </div>
        <!-- Three Right Dashboard icons -->
        <div class="header-tab">
          <div class="">
            <a href="#"
              ><img src="@/assets/icons/notifications-1.svg" alt=""
            /></a>
          </div>
          <div>
            <a h ref="#"><img src="@/assets/icons/help-1.svg" alt="" /></a>
          </div>
          <div class='text-end'>
            <a href="#"><img src="@/assets/icons/account-1.svg" alt="" /></a>
          </div>
        </div>
      </header>
      <!-- =========== Dashbaord Header Ends ============= -->

      <!-- =========== Dashbaord ContentsTop  Begins ============= -->

      <div class="content-wrapper">
        <div class="content-header">
          <div class="payment-title">Payments</div>
          <div class="header-tab">
            <div class="filter">
              <img src="@/assets/icons/filter.svg" alt="" />
              <span>Filter</span>
            </div>
            <div class="export">
              <img src="@/assets/icons/up-arrow.svg" alt="" />
              <span>Export</span>
            </div>
            <div class="payment">
              <img src="@/assets/icons/plus-icon.svg" alt="" />
              <span>Create Payments</span>
            </div>
          </div>
        </div>
        <!-- =========== Dashbaord Contents Top Ends  ============= -->

        <!-- =========== Dashbaord Payment Details Components ============= -->

        <div style="padding-bottom: 100px">
          <PaymentBoard />
        </div>

        <!-- =========== Dashbaord Payment Details Footer ============= -->

        <div class="content-footer">
          <div>16 results</div>
          <div>
            <button class="previous">Previous</button>
            <button class="next">Next</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      toggleBars: false,
    }
  },

}
</script>

<style lang="scss" scoped>
//  main content styling
.main {
  padding-right: 14px;
  margin-left: 270px;
  position: relative;
  overflow: auto;


 

  //   header syling
  header {
    position: fixed;
    right: 16px;
    left: 270px;
    border-bottom: 1px solid #e3e8ee;
    z-index: 1;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 7px 14px 7px 30px;
    box-sizing: border-box;
    margin-bottom: 30px;
    background: #fff;
    input[type='search'] {
      outline: none;
      border: none;
      padding: 6px 3px;
    }
  }

  // header description styling
  .header-tab {
    flex-direction: row;
    align-items: center;
    display: flex;
    div {
      justify-content: flex-end;
      margin-right: 14px;
    }
  }
  //   .content-wrapper styling
  .content-wrapper {
    min-width: 1000px;
    padding: 80px 30px 0 30px;
    .content-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 15px;
    }
  }
  .filter,
  .export,
  .payment {
    display: flex;
    flex-direction: row;
    align-items: center;
    padding: 6px 8px;
    width: auto;
    height: 29px;
    cursor: pointer;
    background: #ffffff;
    /* Secondary button shadow */

    box-shadow: 0px 2px 5px rgba(60, 66, 87, 0.08),
      0px 0px 0px 1px rgba(60, 66, 87, 0.16), 0px 1px 1px rgba(0, 0, 0, 0.12);
    border-radius: 4px;
    span {
      margin: 0 4px;
    }

    /* Inside Auto Layout */
  }
  .payment {
    background: #5469d4;
    color: #fff;
  }
  .content-footer {
    position: static;
    bottom: 20px;
    left: 0px;
    right: 0px;
    padding: 12px 0;

    display: flex;
    justify-content: space-between;
    align-items: center;
    div {
      display: inline-flex;
      flex-direction: row;
      margin-right: 10px;
    }
    button {
      outline: none;
      border: none;
      cursor: pointer;
    }
    .next,
    .previous {
      /* Auto Layout */
      font-weight: 500;

      display: flex;
      flex-direction: row;
      align-items: center;
      padding: 6px 8px;

      width: auto;
      height: 29px;

      background: #ffffff;
      opacity: 0.5;
      /* Secondary button shadow */

      box-shadow: 0px 2px 5px rgba(60, 66, 87, 0.08),
        0px 0px 0px 1px rgba(60, 66, 87, 0.16), 0px 1px 1px rgba(0, 0, 0, 0.12);
      border-radius: 4px;
      margin-right: 8px;

      /* Inside Auto Layout */
    }
    .previous {
      color: #3c4257;
    }
    .next {
      color: #000 !important;
    }
  }
  .payment-title {
    color: #1a1f36;
    font-size: 28px;
    font-weight: bold;
  }
}
@media screen and (max-width: 640px) {
  .main {
    margin-left: 0;
    transition: width 0.2s linear;
    header {
      left: 0;
      transition: width 0.2s linear;
    }
  }
}
</style>
