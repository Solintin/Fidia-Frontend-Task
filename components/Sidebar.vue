<template>
  <div>
    <div
      :class="[isOpen ? 'isOpen' : null, 'toggle-menu']"
      @click="openSideBar"
    >
      <fa :icon="['fas', isOpen ? 'angle-left' : 'angle-right']" class="icon" />
    </div>
    <div :class="[isOpen ? 'isOpen' : null, 'sidebar']">
      <div class="sidebar-content">
        <div>
          <div class="header">
            <div>
              <img src="@/assets/icons/Store-icon.svg" alt="store-icon" />
            </div>
            <div>
              <!-- Top DropDOwn -->
              <select name="dropdown" class="dropdown fs-5">
                <option value="store-name">Store Name</option>
                <option value="store-name">Other Option</option>
                <option value="store-name">Other Option</option>
              </select>
            </div>
          </div>

          <!--  Sidebar Links Rendering Dynamically-->
          <div class="contents-list">
            <div v-for="(link, id) in data" :key="id">
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
            <!-- Toggle Switch  -->
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
import data from '~/Data/Contents.js'
export default {
  data() {
    return {
      data: data,
      onSwitch: false,
      isOpen: false,
    }
  },
  methods: {
    // Toggle Switch Methods
    toggleSwitch() {
      this.onSwitch = !this.onSwitch
    },
    openSideBar() {
      this.isOpen = !this.isOpen
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
  z-index: 100;
  height: 100%;
  overflow: auto;
  position: fixed;
  min-width: 270px;
  left: 0;
  top: 0;
  bottom: 0;
  line-height: 17px;
  box-sizing: border-box;
  transition: all 0.2s linear;

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
  .dropdown{
    font-weight: 600;
    font-size: 15px;
  }
  img {
    height: 40%;
    margin-left: -4px;
  }
  .contents-list {
    display: flex;
    flex-direction: column;
    font-size: 15px;
    line-height: 20px;

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
      font-size: 15px;
      &:last-child {
        margin-bottom: 20px;
      }
    }
  }
  .developers {
    margin-top: 8px;
  }
  .settings {
    margin: 8px 0;
  }
}
.toggle-menu {
  cursor: pointer;
  position: fixed;
  height: 40px;
  width: 40px;
  left: 270px;
  z-index: 2;
  background: royalblue;
  border-radius: 50%;
  top: 50%;
  transform: translate(-40%, -50%);
  display: flex;
  justify-content: center;
  padding-left: 13px;
  align-items: center;
  color: #000;
  background: #f7fafc;
  display: none;
  box-shadow: 0px 2px 5px rgba(60, 66, 87, 0.08),
    0px 0px 0px 1px rgba(60, 66, 87, 0.16), 0px 1px 1px rgba(0, 0, 0, 0.12);
}
.icon {
  font-size: 20px;
}
// Toggle Switch Styling
.switch {
  height: 15px;
  width: 28px;
  background: #e3e8ee;
  border: 1px solid #d9dce1;
  box-sizing: border-box;
  border-radius: 26px;
  margin-left: -5px;
  margin-right: 6px;
  margin-top: 7px;
  .inner-switch {
    height: 15px;
    width: 14px;
    background: #fff;
    border: 1px solid #d9dce1;
    box-sizing: border-box;
    border-radius: 26px;
    margin-top: -1px;
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

@media screen and (max-width: 640px) {
  .toggle-menu {
    display: flex;
  }
  .sidebar {
    left: -100vw;
    transition: all 0.2s linear;
    &.isOpen {
      left: 0;
    }
  }
  .toggle-menu {
    left: 0;
    transition: all 0.2s linear;
    &.isOpen {
      left: 270px;
    }
  }
}
</style>
