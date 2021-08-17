<template>
  <div>
    <div class="sidebar">
      <div class="sidebar-content">
        <div>
          <div class="header">
            <div>
              <img src="@/assets/icons/Store-icon.svg" alt="store-icon" />
            </div>
            <div>
              <select name="dropdown">
                <option value="store-name">Store Name</option>
                <option value="store-name">Other Option</option>
                <option value="store-name">Other Option</option>
              </select>
            </div>
          </div>

          <div class="contents-list">
            <div v-for="link in data" :key="link">
              <div class="link-list">
                <img :src="require(`@/assets/icons/${link.icon}`)" alt="icon" />
                <div>
                  <a :class="[link.state ? 'active' : '']" href="#">
                    {{ link.mainLink }}</a
                  >
                </div>
              </div>

              <ul>
                <li
                  class="sub-list"
                  v-for="(sub, id) in link.sublinks"
                  :key="id"
                >
                  {{ sub }}
                </li>
              </ul>
            </div>

            <div class="link-list developers">
              <img src="@/assets/icons/payments-2.svg" alt="icon" />
              <div>
                <a href="#">Developers</a>
              </div>
            </div>
            <div class="link-list settings">
              <div class="switch">
                <div
                  @click="toggleSwitch"
                  :class="[onSwitch ? 'active' : null, 'inner-switch']"
                ></div>
              </div>
              <div>
                <a href="#">View test data</a>
              </div>
            </div>
            <div class="link-list">
              <img src="@/assets/icons/settings-1.svg" alt="icon" />
              <div>
                <a href="#">settings</a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import data from './Contents.js'
export default {
  data() {
    return {
      data: data,
      onSwitch: false,
    }
  },
  methods: {
    toggleSwitch() {
      this.onSwitch = !this.onSwitch
    },
  },
}
</script>

<style lang="scss" scoped>
.sidebar {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  padding: 12px 20px 0px;

  position: fixed;
  width: 270px;
  height: 900px;
  left: 0px;
  top: 0px;
  box-sizing: border-box;

  /* Grey 100 */

  background: #f7fafc;
  box-shadow: inset -1px 0px 0px #e3e8ee;

  /* Inside Auto Layout */

  flex: none;
  order: 0;
  flex-grow: 0;
  margin: 0px 0px;

  .header {
    display: flex;
    flex-direction: row;
    align-items: center;
    margin-bottom: 20px;
    select {
      background: transparent;
      border: none;
      outline: none;
    }
    div {
      margin-right: 5px;
    }
  }
  img {
    height: 40%;
    margin-left: -4px;
  }
  .contents-list {
    display: flex;
    flex-direction: column;
    font-size: 14px;

    div:first-child {
      margin-bottom: 10px;
    }

    .link-list {
      display: flex;
      align-items: center;
      flex-direction: row;
      margin-left: 10px;

      img {
        margin-right: 16.06px;
        margin-top: -5px;
      }
      a.active {
        color: #7a73ff;
      }
    }

    .sub-list {
      display: flex;
      flex-direction: column;
      margin-left: 37px;
      margin-top: 5px;
      &:last-child {
        margin-bottom: 20px;
      }
    }
  }
  .developers {
    margin-top: 10px;
  }
  .settings {
    margin: 10px 0;
  }
}

.switch {
  height: 15px;
  width: 30px;
  background: #e3e8ee;
  border: 1px solid #d9dce1;
  box-sizing: border-box;
  border-radius: 26px;
  margin-left: -5px;
  margin-right: 10px;
  margin-top: 5px;
  .inner-switch {
    height: 15px;
    width: 15px;
    background: #fff;
    border: 1px solid #d9dce1;
    box-sizing: border-box;
    border-radius: 26px;
    margin-top: -2px;
    margin-left: -2px;
    transition: all 0.28s linear;
    cursor: pointer;

    &.active {
      margin-left: 15px;
      transition: all 0.28s linear;
      background: #7a73ff;
      cursor: pointer;
    }
  }
}
</style>
