<template>
  <md-toolbar
    id="toolbar"
    md-elevation="0"
    class="md-transparent md-absolute"
    style="background: black !important"
  >
    <!--///////////////////////////-ESCRITORIO-/////////////////////////////////////-->
    <section v-if="showDownload" class="sectionFlex">
      <md-button
        class="md-just-icon md-simple md-toolbar-toggle eliminarNavbar moverBoton"
        :class="{ toggled: toggledClass }"
        @click="toggleNavbarMobile()"
      >
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
      </md-button>

      <md-list-item
        class="eliminarMobile"
        href="#/history"
        @click="scrollToElement()"
      >
        <p class="centrarMobile textoNavbar">History</p>
      </md-list-item>

      <md-list-item
        class="eliminarMobile"
        href="#/#team"
        @click="scrollToElement()"
      >
        <p class="centrarMobile textoNavbar">Team</p>
      </md-list-item>

      <md-button
        :class="Logo"
        class="md-simple raikumo"
        href="/raikumo"
        @click="scrollToElement()"
      ></md-button>

      <md-list-item
        class="eliminarMobile"
        href="#/#FAQ"
        @click="scrollToElement()"
      >
        <p class="centrarMobile textoNavbar">FAQ</p>
      </md-list-item>

      <md-list-item
        class="eliminarMobile"
        href="#/#join"
        @click="scrollToElement()"
      >
        <p class="centrarMobile textoNavbar">Jobs</p>
      </md-list-item>
    </section>

    <li class="md-list-item eliminarMobile">
      <a
        href="javascript:void(0)"
        class="md-list-item-router md-list-item-container md-button-clean dropdown"
      >
        <div class="md-list-item-content">
          <drop-down direction="down" class="profile-photo">
            <div
              class="profile-photo-small"
              slot="title"
              data-toggle="dropdown"
            >
              <img :src="Perfil" alt="Circle Image" />
            </div>
            <ul class="dropdown-menu dropdown-menu-right">
              <li class="dropdown-header">You account</li>
              <li>
                <a
                  href="#"
                  class="dropdown-item blanco"
                  style="background: none !important; box-shadow: none !important"
                >
                  Wallet
                </a>
              </li>
              <li>
                <a
                  href="#"
                  class="dropdown-item blanco"
                  style="background: none !important; box-shadow: none !important"
                >
                  Settings and other stuff
                </a>
              </li>
              <li>
                <a
                  href="#"
                  class="dropdown-item blanco azul"
                  style="background: none !important; box-shadow: none !important"
                >
                  Sign Out
                </a>
              </li>
            </ul>
          </drop-down>
        </div>
      </a>
    </li>
    <!--
    <md-list class="eliminarMobile">
      <md-list-item href="javascript:void(0)" @click="scrollToElement()">
        <i class="material-icons">account_circle</i>
        <p class="hidden-lg">Near Wallet</p>
        <md-tooltip md-direction="bottom">You Account</md-tooltip>
      </md-list-item>
    </md-list>-->

    <!--///////////////////////////-MOBILE-/////////////////////////////////////-->
    <div class="md-toolbar-row md-collapse-lateral">
      <div class="md-collapse">
        <div class="md-collapse-wrapper">
          <mobile-menu nav-mobile-section-start="true">
            <md-list-item href="#/history" @click="scrollToElement()">
              <p class="centrarMobile">History</p>
            </md-list-item>
            <md-list-item href="#/#team" @click="scrollToElement()">
              <p class="centrarMobile">Team</p>
            </md-list-item>
            <md-list-item href="#/#FAQ" @click="scrollToElement()">
              <p class="centrarMobile">FAQ</p>
            </md-list-item>
            <md-list-item href="#/#join" @click="scrollToElement()">
              <p class="centrarMobile">Jobs</p>
            </md-list-item>

            <li class="md-list-item">
              <a
                href="javascript:void(0)"
                class="md-list-item-router md-list-item-container md-button-clean dropdown"
              >
                <div class="md-list-item-content">
                  <drop-down direction="down" class="profile-photo">
                    <div
                      class="profile-photo-small centrarMobile"
                      slot="title"
                      data-toggle="dropdown"
                    >
                      <img :src="Perfil" alt="Circle Image" />
                    </div>
                    <ul class="dropdown-menu dropdown-menu-right">
                      <li class="dropdown-header">You account</li>
                      <li>
                        <a
                          href="#"
                          class="dropdown-item blanco"
                          style="background: none !important; box-shadow: none !important"
                        >
                          Wallet
                        </a>
                      </li>
                      <li>
                        <a
                          href="#"
                          class="dropdown-item blanco azul"
                          style="background: none !important; box-shadow: none !important"
                        >
                          Settings and other stuff
                        </a>
                      </li>
                      <li>
                        <a
                          href="#"
                          class="dropdown-item blanco azul"
                          style="background: none !important; box-shadow: none !important"
                        >
                          Sign Out
                        </a>
                      </li>
                    </ul>
                  </drop-down>
                </div>
              </a>
            </li>
          </mobile-menu>
        </div>
      </div>
    </div>
  </md-toolbar>
</template>

<script>
let ubicacionPrincipal = window.pageYOffset;
let resizeTimeout;
function resizeThrottler(actualResizeHandler) {
  // ignore resize events as long as an actualResizeHandler execution is in the queue
  if (!resizeTimeout) {
    resizeTimeout = setTimeout(() => {
      resizeTimeout = null;
      actualResizeHandler();

      // The actualResizeHandler will execute at a rate of 15fps
    }, 80);
  }
}
import MobileMenu from "@/layout/MobileMenu";
export default {
  data() {
    return {
      toggledClass: false
    };
  },
  components: {
    MobileMenu
  },
  props: {
    perfil: {
      type: String,
      default: require("@/assets/team/monkey.jpg")
    }
  },
  computed: {
    Logo() {
      return {
        logoRaikumo: true
      };
    },
    Perfil() {
      return `${this.perfil}`;
    },
    showDownload() {
      const excludedRoutes = ["login", "landing", "profile"];
      return excludedRoutes.every(r => r !== this.$route.name);
    }
  },
  methods: {
    bodyClick() {
      let bodyClick = document.getElementById("bodyClick");

      if (bodyClick === null) {
        let body = document.querySelector("body");
        let elem = document.createElement("div");
        elem.setAttribute("id", "bodyClick");
        body.appendChild(elem);

        let bodyClick = document.getElementById("bodyClick");
        bodyClick.addEventListener("click", this.toggleNavbarMobile);
      } else {
        bodyClick.remove();
      }
    },
    toggleNavbarMobile() {
      this.NavbarStore.showNavbar = !this.NavbarStore.showNavbar;
      this.toggledClass = !this.toggledClass;
      this.bodyClick();
    },
    scrollToElement() {
      let element_id = document.getElementById("downloadSection");
      if (element_id) {
        element_id.scrollIntoView({ block: "end", behavior: "smooth" });
      }
    },
    OcultarNavbar() {
      let Desplazamiento_Actual = window.pageYOffset;
      if (ubicacionPrincipal >= Desplazamiento_Actual) {
        document.getElementById("toolbar").style.top = "0";
      } else {
        document.getElementById("toolbar").style.top = "-100px";
      }
      ubicacionPrincipal = Desplazamiento_Actual;
    },
    scrollListener() {
      resizeThrottler(this.OcultarNavbar);
    }
  },
  mounted() {
    document.addEventListener("scroll", this.scrollListener);
  },
  beforeDestroy() {
    document.removeEventListener("scroll", this.scrollListener);
  }
};
</script>

<style scoped>
*{z-index:10}.blanco{color:#fff !important}.sectionFlex{justify-content:center;width:90%;display:flex}.raikumo{position:relative;width:20%}.logoRaikumo{background:center no-repeat url("../assets/logos/raikumo long.png");background-size:cover}.centrarMobile{margin:auto !important}.eliminarMobile{display:block;margin:0 10px}.eliminarNavbar{display:none}.foto{background:center no-repeat;background-size:cover}.moverBoton{position:absolute !important;top:10%}.textoNavbar{font-size:1.125rem !important}
</style>
