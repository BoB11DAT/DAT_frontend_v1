<template>
  <header>
    <NuxtLink :to="{ path: '/' }" class="logo"
      ><img src="~/assets/imgs/logo.svg"
    /></NuxtLink>
    <template v-for="(i, n) in headerItems" :key="n">
      <NuxtLink :to="{ path: i.path }" class="header_item">{{ i.content }}</NuxtLink>
    </template>
    <a href="https://pdf.datg.xyz" target="_blank" class="header_item"> PDF </a>
    <a href="https://doc.datg.xyz" target="_blank" class="header_item">
      DocDoc
    </a>
    <template v-if="store.getAccessToken">
      <NuxtLink :to="{ path: '/mypage/' }" class="my_page"
        >마이 페이지</NuxtLink
      >
      <button class="logout" @click="logoutAction()">로그아웃</button>
    </template>
    <template v-else>
      <NuxtLink :to="{ path: '/login/' }" class="login">로그인</NuxtLink>
      <NuxtLink :to="{ path: '/register/' }" class="register"
        >회원가입
      </NuxtLink>
    </template>
  </header>
</template>

<script setup>
import { useCookie } from "#app";
import { useRouter } from "vue-router";
import headerItems from "~/constants/headerItems";
import { useAuthStore } from "~/store/auth";
import { logout } from "~/api/auth";

// eslint-disable-next-line no-undef
const config = useRuntimeConfig();

const store = useAuthStore();
const router = useRouter();

function logoutAction() {
  logout();
  store.setAccessToken("");
  router.push("/");
}
</script>

<style lang="scss" scoped>
@import "~/assets/styles/components/header/style.scss";
</style>
