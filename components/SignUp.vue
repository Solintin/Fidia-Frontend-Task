<template>
  <div>
    <div class="sign-in-card">
      <div class="sign-in-container">
        <h1>Sign in to your account</h1>
        <div class="form-field">
          <form @submit.prevent>
            <div class="form-input">
              <label for="email"> Email </label>
              <div class="input-wrap">
                <input
                  type="email"
                  name="email"
                  v-model.trim="email"
                  required
                  placeholder="jane.doe@gmail.com"
                />
              </div>
            </div>

            <div class="form-input">
              <div class="password-field">
                <label for="email"> Password </label>

                <span> <a href="#"> Forgot Password </a> </span>
              </div>
              <div class="input-wrap">
                <input
                  required
                  type="password"
                  id="password"
                  v-model.trim="password"
                  placeholder="Password"
                />
                <div class="input-icon" @click="switchVisibility">
                  <span v-if="passwordVisible">
                    <fa :icon="['fas', 'eye']" />
                  </span>
                  <span v-else>
                    <fa :icon="['fas', 'eye-slash']" />
                  </span>
                </div>
              </div>
            </div>

            <div class="check-input">
              <input type="checkbox" checked />
              <span>Stay signed in for a week</span>
            </div>

            <div class="form-input" @click="logIn">
              
              <button >
                  <span v-if="loader">
                <Loading />
              </span>
                  <span v-else>Continue</span>
                  </button>
            </div>

            <div class="alternative-auth">
              <a href="#"> Use single sign-on (SSO) instead</a>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      loader: false,
      email: '',
      password: '',
      passwordVisible: false,
    }
  },
  methods: {
    switchVisibility() {
      this.passwordVisible = !this.passwordVisible
      const passwordField = document.querySelector('#password')
      if (passwordField.getAttribute('type') === 'password')
        passwordField.setAttribute('type', 'text')
      else passwordField.setAttribute('type', 'password')
    },
    logIn() {
      this.loader = !this.loader
      setTimeout(() => {
        this.$nuxt.$options.router.push('/dashboard')
        this.loader = !this.loader
      }, 1500)
      
    },
  },
}
</script>

<style lang="scss" scoped>
.sign-in-card {
  border-radius: 4px;
  box-shadow: 0px 5px 15px rgba(0, 0, 0, 0.12),
    0px 15px 35px rgba(60, 66, 87, 0.08);
  overflow: hidden;
  background-color: #fff;
  flex-shrink: 0;
  box-sizing: border-box;
  padding: 56px 48px;

  .sign-in-container {
    padding-right: 20px;
    padding-left: 20px;

    .form-field {
      padding-top: 20px;
      // padding-left: 20px;
      display: flex;
      flex-direction: column;

      form {
        &label {
          margin-bottom: 12px;
        }
        .form-input {
          margin-bottom: 30px;
          a {
            color: #7a73ff;
          }

          .password-field {
            display: flex;
            justify-content: space-between;
          }
          button {
            margin-top: 10px;
            padding: 13.5px 10px;

            border-radius: 5px;
            background: #7a73ff;
            text-align: center;
            min-width: 100%;
            color: #fff;
            outline: none;
            border: none;
            cursor: pointer;
          }
        }
        .input-wrap {
          min-height: 40px;
          border: 1px solid #d9dce1;
          box-sizing: border-box;
          border-radius: 5px;
          margin-top: 10px;
          position: relative;
          .input-icon {
            position: absolute;
            top: 10px;
            right: 5px;
            cursor: pointer;
          }
        }
        input[type='email'],
        input[type='password'],
        input[type='text'] {
          padding: 12px 16px;
          background-color: rgb(255, 255, 255);
          min-width: 100%;
          border: none;
          outline: none;
          border-radius: 5px;
          box-sizing: border-box;
          min-height: 100%;
        }

        .check-input {
          display: flex;
          margin-bottom: 12px;
          flex-direction: row;
          align-items: center;
          span {
            font-size: 14px;
            margin-left: 10px;
            color: #3c4257;
          }
        }
        .alternative-auth {
          display: flex;
          margin-top: 15px;
          flex-direction: row;
          align-items: center;
          justify-content: center;
          a {
            color: #7a73ff;
          }
        }
      }
    }
  }
}
</style>
