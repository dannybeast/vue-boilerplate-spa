<template lang="pug">
  include ../../utils/bem/index.pug
  +b.HEADER.header
    .container-fluid
      +e.row
        +e.ROUTER-LINK(to="/" class="logo")
          img(:src="logoUrl", :alt="slogan")
          +e.H1.slogan {{slogan}}
        router-link(to="/secret") Secret
        user-profile(v-if="isAuth")

</template>

<script>
import { mapState, mapGetters } from "vuex";
import UserProfile from "@/components/ui/UserProfile";
export default {
  name: "TheHeader",
  data() {
    return {
      slogan: "Запрос и оценка инфраструктуры",
      logoUrl: "/images/logo.svg"
    };
  },
  computed: {
    ...mapGetters({ isAuth: "Auth/isAuthenticated" })
  },
  components: {
    UserProfile
  }
};
</script>

<style lang="scss">
.header {
  background: #fff;
  width: 100%;
  box-shadow: $shadowBase;
  padding: 15px 0;
  position: relative;
  z-index: 3;
  &__row {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  &__logo {
    display: flex;
    align-items: center;
    text-decoration: none;
    img {
      width: 40px;
      margin-right: 25px;
    }
  }
  &__slogan {
    font-size: 14px;
    line-height: $mainLineHeight;
    font-weight: 400;
    color: $mainFontColor;
    max-width: 220px;
    margin-right: auto;
  }
}
</style>
