<script setup>
import index from './components/main.vue'
import {onMounted, provide, ref} from "vue";

const navMenu = ref({
  menu1: false, menu2: false, menu3: false, menu4: false
})

const first = ref([
  {
    name: "🐈貓車折扣",
    routerPath: "#",
  },
  {
    name: "🐈貓車新品",
    routerPath: "#",
  },
  {
    name: "🐈貓車特色",
    routerPath: "#",
  },
])

const second = ref([
  {
    name: "🐈最新到貨",
    routerPath: "#",
  },
  {
    name: "🐈人氣推薦",
    routerPath: "#",
  },
])

const third = ref([
  {
    name: "🐈福箱專區",
    routerPath: "#",
  },
])

</script>

<style scoped lang="scss">

* {
  margin: 0;
  padding: 0;
}

nav {
  background-color: #e4dab8;
  padding: 0 20px;

  border-top-left-radius: 10px;
  border-top-right-radius: 10px;

  a {
    text-decoration: none;
    color: inherit;
  }

  ul {
    margin: 0;
    padding: 0;
    list-style: none;

    .first {
      margin-right: 50px;
      margin-left: 10px;
    }

    li {
      position: relative;
      display: inline-block;
      padding: 15px 20px;
      color: #000000;
      cursor: pointer;
      transition: background-color 0.3s;

      input {
        border: none;
        outline: none;
        width: 300px;
        height: 35px;
        font-size: 16px;
      }

      button {
        border: solid 1px #666;
        background-color: #666;
        color: white;
        padding: 10px;
        cursor: pointer;
        height: 35px;
      }

      &:hover {
        background-color: #e0d09c;
      }
    }
  }
}

.slide-fade-enter-active {
  transition: all 0.3s ease-in-out;
}

.slide-fade-leave-active {
  transition: all 0.3s cubic-bezier(1, 0.5, 0.8, 1);
}

.slide-fade-enter-from,
.slide-fade-leave-to {
  transform: translateY(20px);
  opacity: 0;
}

.menu {
  transform-origin: top center;
  position: absolute;
  top: 100%;
  left: 0;
  min-width: 200px;
  background-color: #fff;
  border-radius: 4px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  z-index: 100;

  li {
    display: block;
    padding: 12px 20px;
    color: #333;
    font-size: 14px;
    border-bottom: 1px solid #eee;
    transition: all 0.3s ease;

    &:last-child {
      border-bottom: none;
    }

    &:hover {
      background-color: #f8f9fa;
      color: #2c3e50;
      padding-left: 25px;
    }
  }
}

</style>

<template>
  <nav ref="onClick">
    <ul>
      <li class="first">
        <router-link to="/">歡迎來到🐈貓車聚集地CART(回到主頁)</router-link>
        </li>
      <li>
        <form @submit="provide()">
          <input type="text" placeholder="搜尋商品..."/>
          <button>搜尋</button>
        </form>
      </li>
      <li><router-link to="#">🐈全部商品</router-link></li>
      <li>
        <router-link to="#" @mouseenter="navMenu.menu1=true" @mouseleave="navMenu.menu1=false">🐈貓車周年慶</router-link>
        <Transition name="slide-fade">
          <ul class="menu" v-show="navMenu.menu1">
            <li v-for="(f, index) in first" :key="index" @mouseenter="navMenu.menu1=true" @mouseleave="navMenu.menu1=false">
              <router-link :to="f.routerPath">{{ f.name }}</router-link>
            </li>
          </ul>
        </Transition>
      </li>
      <li>
        <router-link to="#" @mouseenter="navMenu.menu2=true" @mouseleave="navMenu.menu2=false">🐈吉伊卡哇</router-link>
        <Transition name="slide-fade">
          <ul class="menu" v-show="navMenu.menu2">
            <li v-for="(s, index) in second" :key="index" @mouseenter="navMenu.menu2=true" @mouseleave="navMenu.menu2=false">
              <router-link :to="s.routerPath">{{ s.name }}</router-link>
            </li>
          </ul>
        </Transition>
      </li>
      <li>
        <router-link to="#" @mouseenter="navMenu.menu3=true" @mouseleave="navMenu.menu3=false">🐈貓車福箱</router-link>
        <Transition name="slide-fade">
          <ul class="menu" v-show="navMenu.menu3">
            <li v-for="(t, index) in third" :key="index" @mouseenter="navMenu.menu3=true" @mouseleave="navMenu.menu3=false">
              <router-link :to="t.routerPath">{{ t.name }}</router-link>
            </li>
          </ul>
        </Transition>
      </li>
      <li>
        <router-link to="#" @mouseenter="navMenu.menu4=true" @mouseleave="navMenu.menu4=false">🐈個人中心</router-link>
        <Transition name="slide-fade">
          <ul class="menu" v-show="navMenu.menu4">
            <li @mouseenter="navMenu.menu4=true" @mouseleave="navMenu.menu4=false">
              <router-link to="/login">🐈帳號登入</router-link>
            </li>
            <li @mouseenter="navMenu.menu4=true" @mouseleave="navMenu.menu4=false">
              <router-link to="/reg">🐈帳號註冊</router-link>
            </li>
          </ul>
        </Transition>
      </li>
    </ul>
  </nav>

  <router-view />
</template>
