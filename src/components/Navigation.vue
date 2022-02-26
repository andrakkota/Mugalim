<template>
  <header :class="{ 'scrolled-nav': scrollNav }">
    <nav>
      <div class="logo">
        <router-link :to="{name: 'home'}"><img src="@/assets/logo.png" alt="logo" /> </router-link>

      </div>
      <ul v-show="!mobile" class="navigation">
        <li><router-link class="link" :to="{name: ''}">Все курсы</router-link></li>
        <li><router-link class="link" :to="{name: ''}">О центре</router-link></li>
        <li><router-link class="link" :to="{name: ''}">Новости</router-link></li>
        <li><router-link class="link" :to="{name: ''}">Фотогалерея</router-link></li>
        <li><router-link class="link" :to="{name: ''}">Войти</router-link></li>
      </ul>
      <div @click="toggleMobileNav" v-show="mobile"  class="icon" :class="{ 'icon-active': mobileNav }">
        <img src="@/assets/burger.svg" alt="">
      </div>
      <transition name="mobile-nav">
        <ul v-show="mobileNav" class="dropdown-nav">
          <li><router-link class="link" :to="{name: 'home'}">Главная</router-link></li>
          <li><router-link class="link" :to="{name: ''}">Все курсы</router-link></li>
          <li><router-link class="link" :to="{name: ''}">О центре</router-link></li>
          <li><router-link class="link" :to="{name: ''}">Новости</router-link></li>
          <li><router-link class="link" :to="{name: ''}">Фотогалерея</router-link></li>
          <li><router-link class="link" :to="{name: ''}">Войти</router-link></li>
        </ul>
      </transition>
    </nav>
  </header>
</template>

<script>
export default {
  name: "navigation",
  data() {
    return {
      scrollNav: null,
      mobile: null,
      mobileNav: null,
      windowWidth: null,
    };
  },
  created() {
    window.addEventListener('resize', this.checkScreen);
    this.checkScreen();
  },

  mounted() {
    window.addEventListener('scroll', this.updateScroll);
  },

  methods: {
    toggleMobileNav() {
      this.mobileNav = !this.mobileNav;
    },

    updateScroll() {
      const scrollPosition = window.scrollY;
      if (scrollPosition > 50){
        this.scrollNav = true;
        return;
      }
      this.scrollNav = false;
    },


    checkScreen() {
      this.windowWidth = window.innerWidth;
      if (this.windowWidth <= 750){
        this.mobile = true;
        return;
      }
      this.mobile = false;
      this.mobileNav = false;
      return;
    },
  }
};
</script>

<style lang="scss" scoped>

header  {
  z-index: 99;
  width: 100%;
  position:fixed;
  transition: .5s ease all;
  color: #fff;

  nav {
    position: relative;
    display: flex;
    flex-direction: row;
    padding: 12px 0;
    transition: .5s ease all;
    width: 90%;
    margin: 0 auto;
    @media(min-width:1140px) {
      max-width: 1140px;
    }

    ul,
    .link {
      font-weight: 500;
      color: #000;
      list-style: none;
      text-decoration: none;
    }

    li {
      text-transform: uppercase;
      padding: 16px;
      margin-left: 16px;
    }

    .link {
      font-size: 14px;
      -webkit-transition: .5s ease all;
      -moz-transition: .5s ease all;
      -ms-transition: .5s ease all;
      -o-transition: .5s ease all;
      transition: .5s ease all;
      border-bottom: 1px solid transparent;

      &:hover {
        color: #b214be;
        border-radius: 3px;
        border-color: #b214be;
      }
    }

    .logo {
      display: flex;
      align-items: center;

      img {
        width: 50px;
        transition: .5s ease all;
      }
    }

    .navigation   {
      display: flex;
      align-items: center;
      flex: 1;
      justify-content: flex-end;
    }

    
    .icon {
      cursor: pointer;
      display: flex;
      align-items: center;
      position: absolute;
      right: 24px;
      top:0;
      height: 100%;


      img {
        width: 30px;
        height: 50px;
        transition: .8s ease all;
      }
    }

    .icon-active {
      transform: rotate(180deg);
    }

    .dropdown-nav {
      display: flex;
      flex-direction: column;
      position: fixed;
      width: 100%;
      max-width: 250px;
      height: 100%;
      background: #fff;
      top: 0;
      left: 0;

      li {
        margin-left: 0;
        .link {
          color: #000;
        }
      }
    }

    .mobile-nav-enter-active,
    .mobile-nav-leave-active {
        transition: 1s ease all;
    }

    .mobile-nav-enter-from,
    .mobile-nav-leave-to {
      transform: translateX(-250px);
    }

    .mobile-nav-enter-to {
      transform: translateX(0);
    }

  }

}

.scrolled-nav {
  background-color: #dedede;
  box-shadow: 0 4px 6px -1px rgba(0,0,0,0.1), 0 2px 4px -1px rgba(0,0,0, 0.06);

  nav {
    padding: 8px 0;

    .logo {
      img {
        width: 40px;
        box-shadow: 0 4px 6px -1px rgba(0,0,0,0.1), 0 2px 4px -1px rgba(0,0,0, 0.06);
      }
    }
  }
}

</style>