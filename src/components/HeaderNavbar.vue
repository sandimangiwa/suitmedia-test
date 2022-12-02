<template>
  <div>
    <b-navbar
      id="navbar"
      fixed="top"
      toggleable="lg"
      type="dark"
      style="
        background-color: #ff6404;
        -webkit-transition: all 0.15s linear;
        transition: all 0.15s linear;
        will-change: background, transform;
      "
    >
      <div class="container">
        <b-navbar-brand to="/">
          <img height="40px" src="../assets/logo.png" alt="suitmedia" />
        </b-navbar-brand>
        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

        <b-collapse id="nav-collapse" is-nav>
          <!-- Right aligned nav items -->
          <b-navbar-nav class="ml-auto">
            <b-nav-item
              active-class="active"
              class="nav-link"
              v-for="routes in links"
              :key="routes.id"
              :to="routes.path"
            >
              {{ routes.name }}
            </b-nav-item>
          </b-navbar-nav>
        </b-collapse>
      </div>
    </b-navbar>
  </div>
</template>

<script>
export default {
  name: "HeaderNavbar",
  data() {
    return {
      links: [
        {
          id: 0,
          name: "Work",
          path: "/work",
        },
        {
          id: 1,
          name: "About",
          path: "/about",
        },
        {
          id: 2,
          name: "Services",
          path: "/services",
        },
        {
          id: 3,
          name: "Ideas",
          path: "/ideas",
        },
        {
          id: 4,
          name: "Careers",
          path: "/careers",
        },
        {
          id: 5,
          name: "Contact",
          path: "/contact",
        },
      ],
    };
  },
  mounted() {
    var prevScrollpos = window.pageYOffset;
    window.onscroll = function () {
      var currentScrollPos = window.pageYOffset;
      if (currentScrollPos < 50) {
        document.getElementById("navbar").style.backgroundColor =
          "rgba(255, 100, 4)";
      } else if (prevScrollpos > currentScrollPos) {
        document.getElementById("navbar").style.top = "0";
        document.getElementById("navbar").style.backgroundColor =
          "rgba(255, 100, 4,0.9)";
      } else {
        document.getElementById("navbar").style.top = "-80px";
      }
      prevScrollpos = currentScrollPos;
    };
  },
};
</script>

<style>
.active {
  border-bottom: solid white 2px;
}
</style>
