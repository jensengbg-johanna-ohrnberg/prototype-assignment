<template>
  <div>
    <section class="settings-desktop" v-if="!isMobile">
        <img class="exit-button" @click="goToStartPage()" src="../assets/close-button.png">
        <SettingsMenuDesktop class="settings-menu" />
        <ChangeLanguageDesktop class="change-language" />
    </section>
    <div class="menu" v-else>
      <SettingsNav />
      <h2>Settings</h2>
      <ul>
        <li class="selectDiv">
          <select name="languages" id="">
            <option value="english">English</option>
            <option value="Swahili">Swahili</option>
            <option value="Kikuyu">Kikuyu</option>
            <option value="Luo">Luo</option>
            <option value="Akamba">Akamba</option>
            <option value="Maa">Maa</option>
          </select>
        </li>
        <li>
          <button class="btn" @click="navToSecurity">Security</button>
        </li>
        <li>
          <button class="btn" @click="navToSupport">Support</button>
        </li>
        <li>
          <button class="btn" @click="navToAbout">About</button>
        </li>
        <li>
          <section class="switches">
            <div class="switch">
              <label for="notification">
                <p>Notification</p>
              </label>
              <div>
                <input type="checkbox" name="notification" id="" />
                <div class="slider"></div>
              </div>
            </div>
            <div class="switch">
              <label for="sound">
                <p>Sound</p>
              </label>
              <div>
                <input type="checkbox" name="sound" id="" checked />
                <div class="slider"></div>
              </div>
            </div>
          </section>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import SettingsNav from "@/components/settingsComp/SettingsNav.vue"
import SettingsMenuDesktop from "../components/settingsComp/SettingsMenuDesktop.vue"
import ChangeLanguageDesktop from "../components/settingsComp/ChangeLanguageDesktop.vue"

export default {
  components: {
    SettingsNav,
    SettingsMenuDesktop,
    ChangeLanguageDesktop
  },
  data() {
    return {
      isMobile: false
    }
  },
  methods: {
    navToAbout: function() {
      this.$router.push("/settings-about")
    },
    navToSecurity: function() {
      this.$router.push("/settings-security")
    },
    navToSupport: function() {
      this.$router.push("/settings-support")
    },
    goToStartPage() {
      this.$router.push({ path: '/' });
    },
    windowResize() {
      let windowWidth = window.innerWidth;

      if(windowWidth < 768) {
        this.isMobile = true;
      } else {
        this.isMobile = false;
      }
    }
  },
  created() {
    window.addEventListener('resize', this.windowResize);
    this.windowResize();
  },
  unmounted() {
    window.removeEventListener('resize', this.windowResize);
  },
}
</script>

<style lang="scss" scoped>
@mixin flex {
  display: flex;
  justify-content: flex-start;
  align-items: center;
}
.menu {
  width: 100vw;
  height: 100vh;
  @include flex();
  flex-direction: column;

  h2 {
    color: #222;
    margin-top: 2rem;
  }

  ul {
    padding: 1rem 2rem;
    width: 100%;
    list-style: none;

    li {
      width: 100%;
      margin: 4rem 0rem;

      .btn,
      select {
        position: relative;
        background: #efefef;
        padding: 1rem 0.5rem;
        width: 100%;
        border-radius: 6rem;
        border: none;
        text-transform: uppercase;
        color: #222;
        font-weight: bold;
        transition: all 0.4s ease;
        cursor: pointer;

        &:hover {
          background: #ec2329;
          color: #fefefe;
        }
      }

      select {
        padding: 1rem 1.5rem;
        appearance: none;
      }
    }

    .selectDiv {
      position: relative;

      &::before {
        content: ">";
        width: 2rem;
        height: 2rem;
        position: absolute;
        font: 17px "Consolas", monospace;
        color: #333;
        top: 40%;
        right: 1rem;
        transform: rotate(90deg);
        z-index: 10;
        pointer-events:none;
      }
    }

    .switches {
      @include flex();
      justify-content: space-between;
      align-items: center;
      padding: 1rem;

      .switch {
        @include flex();
        flex-direction: column;
        min-height: 6rem;

        label {
          @include flex();

          p {
            margin: 1rem;
            text-transform: uppercase;
            font-weight: bold;
          }
        }

        div {
          position: relative;
          width: 40px;
          height: 60px;
          @include flex();
          flex-direction: column;
          justify-content: center;

          .slider {
            position: relative;
            width: 5rem;
            height: 2.7rem;
            border-radius: 5rem;
            background: #e0e0e0;
            transition: all 0.4s ease;
            cursor: pointer;

            &:before {
              position: absolute;
              top: 0.6rem;
              left: 0.6rem;
              content: "";
              background: #fefefe;
              width: 1.6rem;
              height: 1.6rem;
              border-radius: 5rem;
              transition: all 0.4s ease;
              cursor: pointer;
            }
          }

          input {
            position: absolute;
            top: 0;
            left: -10;
            opacity: 0;
            background: red;
            width: 70px;
            height: 50px;
            z-index: 10;
            cursor: pointer;
          }

          input:checked + .slider {
            background-color: #1fab55;
          }

          input:checked + .slider::before {
            transform: translateX(2.3rem);
          }
        }
      }
    }
  }
}
  .settings-desktop {
      display: grid;
      grid-template-columns: 20rem 1fr;
      justify-items: center;
  }

  .exit-button {
      display: block;
      position: absolute;
      top: 2rem;
      right: 2rem;
  }
  .exit-button:hover {
      cursor: pointer;
  }

  .settings-menu {
      grid-column: 1 / 2;
  }

  .change-language {
      grid-column: 2 / 3;
  }
</style>
