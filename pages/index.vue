<template>
  <div>
    <div class="base-layout">
      <div class="layout-container">
        <div class="fixed-background">
          <div class="first-line"></div>
          <div class="second-line"></div>
          <div class="fourth-line"></div>
          <div class="fifth-line"></div>
        </div>
        <div class="skew-background">
          <div class="first-left-stripe"></div>
          <div class="second-left-stripe"></div>
          <div class="left-blend-stripe"></div>
          <div class="first-right-stripe"></div>
        </div>

        <div class="content-container">
          <div class="form-container">
            <div class="logo"><img src="@/assets/icons/logo.svg" alt="" /></div>

            <SignUp />

            <div class="bottom-content">
              <div>
                Don't have an account? <span> <a href="#">sign up</a></span>
              </div>
              <div class="bottom-list">
                <ul>
                  <li><span>&copy; </span>Stripe</li>
                  <li>Contact</li>
                  <li>Privacy & terms</li>
                </ul>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {}
</script>

<style lang="scss" scoped>
.content-container {
  position: relative;

  display: flex;
  flex-direction: row;
  justify-content: center;
  margin: 0 auto;
  height: 100%;
  width: 1080;
  padding-top: 56px;
  box-sizing: border;
  z-index: 0;

  .form-container {
    display: flex;
    flex-direction: column;
    box-sizing: border;
    width: 540px;
    min-width: 540px;

    .logo {
      padding-bottom: 40px;
      padding-left: 20px;
    }

    .bottom-content {

      color: #4F566B;
      font-size: 14px;
      margin: 15px 0;
      padding: 10px 15px;
      display: flex;
      flex-direction: column;
      box-sizing: border;
      a {
        color: #635cff;
      }

      .bottom-list {
        margin-top: 15px;

        ul {
          list-style: circle !important;
        }
        li {
          display: inline-flex;
          margin-right: 5px;
          padding: 3px 0;
          font-weight: 500;
          font-size: 15px;
        }
      }
    }
  }
}
</style>
