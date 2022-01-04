<template>
  <div class="white-skin mdb-admin-sidenav">
    <mdb-side-nav
      logo="https://mdbootstrap.com/img/logo/mdb-transaprent-noshadows.png"
      sideNavClass="sn-bg-4"
      mask="strong"
      :OpenedFromOutside.sync="toggle"
    >
      <li>
        <form class="search-form" role="search">
          <div class="form-group md-form mt-0 pt-1 ripple-parent" @click="wave">
            <input type="text" class="form-control" placeholder="Search" />
          </div>
        </form>
      </li>
      <li>
        <mdb-side-nav-nav>
          <mdb-side-nav-cat name="Dashboards" icon="tachometer-alt">
            <mdb-side-nav-item
              to="/"
              @click.native="width < 1440 && toggleSideNav(false)"
              >Version 1</mdb-side-nav-item
            >
            <mdb-side-nav-item
              to="/dashboards/v-2"
              @click.native="width < 1440 && toggleSideNav(false)"
              >Version 2</mdb-side-nav-item
            >
            <mdb-side-nav-item
              to="/dashboards/v-3"
              @click.native="width < 1440 && toggleSideNav(false)"
              >Version 3</mdb-side-nav-item
            >
            <mdb-side-nav-item
              to="/dashboards/v-4"
              @click.native="width < 1440 && toggleSideNav(false)"
              >Version 4</mdb-side-nav-item
            >
            <mdb-side-nav-item
              to="/dashboards/v-5"
              @click.native="width < 1440 && toggleSideNav(false)"
              >Version 5</mdb-side-nav-item
            >
            <mdb-side-nav-item
              to="/dashboards/v-6"
              @click.native="width < 1440 && toggleSideNav(false)"
              >Version 6</mdb-side-nav-item
            >
          </mdb-side-nav-cat>
          <mdb-side-nav-cat name="Pages" icon="image">
            <mdb-side-nav-item
              @click.native="width < 1440 && toggleSideNav(false)"
              target="_blank"
              to="/pages/login"
              >Login</mdb-side-nav-item
            >
            <mdb-side-nav-item
              @click.native="width < 1440 && toggleSideNav(false)"
              target="_blank"
              to="/pages/register"
              >Register</mdb-side-nav-item
            >
          </mdb-side-nav-cat>

          <mdb-side-nav-cat name="Components" icon="th">
            <mdb-side-nav-item
              class="ripple-parent"
              @click.native="width < 1440 && toggleSideNav(false)"
              to="/components/datepicker"
              >Date picker</mdb-side-nav-item
            >
            <mdb-side-nav-item
              class="ripple-parent"
              @click.native="width < 1440 && toggleSideNav(false)"
              to="/components/timepicker"
              >Time picker</mdb-side-nav-item
            >
          </mdb-side-nav-cat>

          <mdb-side-nav-cat name="Forms" far icon="check-square">
            <mdb-side-nav-item
              class="ripple-parent"
              @click.native="width < 1440 && toggleSideNav(false)"
              to="/forms/basic"
              >Basic</mdb-side-nav-item
            >
            <mdb-side-nav-item
              class="ripple-parent"
              @click.native="width < 1440 && toggleSideNav(false)"
              to="/forms/extended"
              >Extended</mdb-side-nav-item
            >
          </mdb-side-nav-cat>

          <mdb-side-nav-cat name="Tables" icon="table">
            <mdb-side-nav-item
              class="ripple-parent"
              @click.native="width < 1440 && toggleSideNav(false)"
              to="/tables/basic"
              >Basic</mdb-side-nav-item
            >
            <mdb-side-nav-item
              class="ripple-parent"
              @click.native="width < 1440 && toggleSideNav(false)"
              to="/tables/extended"
              >Extended</mdb-side-nav-item
            >
            <mdb-side-nav-item
              class="ripple-parent"
              @click.native="width < 1440 && toggleSideNav(false)"
              to="/tables/datatables"
              >DataTables</mdb-side-nav-item
            >
          </mdb-side-nav-cat>

          <mdb-side-nav-item
            header
            @click.native="width < 1440 && toggleSideNav(false)"
            far
            icon="calendar-check"
            to="/calendar/calendar"
            >Calendar</mdb-side-nav-item
          >
        </mdb-side-nav-nav>
      </li>
    </mdb-side-nav>
  </div>
</template>

<script>
import {
  mdbSideNav,
  mdbSideNavNav,
  mdbSideNavCat,
  mdbSideNavItem,
  waves,
} from "mdbvue";
import { mapGetters, mapActions } from "vuex";

export default {
  name: "SideNav",
  props: {
    waves: {
      type: Boolean,
      default: true,
    },
    open: {
      type: Boolean,
    },
  },
  components: {
    mdbSideNav,
    mdbSideNavNav,
    mdbSideNavCat,
    mdbSideNavItem,
  },
  data() {
    return {
      active: 0,
      elHeight: 0,
      windowHeight: 0,
      toggle: true,
      width: 0,
    };
  },
  computed: mapGetters(["sidenav"]),
  methods: {
    ...mapActions(["toggleSideNav"]),
    afterEnter(el) {
      el.style.maxHeight = "1000px";
    },
    beforeLeave(el) {
      el.style.maxHeight = 0;
    },
    setWidth() {
      this.width = window.innerWidth;
    },
  },
  mounted() {
    this.setWidth();
    window.addEventListener("resize", this.setWidth);
  },
  beforeDestroy() {
    window.removeEventListener("resize", this.setWidth);
  },
  watch: {
    toggle(value) {
      this.toggleSideNav(value);
    },
    sidenav(value) {
      this.toggle = value;
    },
    width(value) {
      if (value < 1440) {
        this.toggle = false;
      } else this.toggle = true;
    },
  },
  mixins: [waves],
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->

<style>
.side-nav {
  opacity: 1 !important;
  transition: transform 0.3s linear !important;
}
</style>
