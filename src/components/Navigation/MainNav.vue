<template>
  <header :class="['w-full', 'text-sm', headerHeightClass]">
    <div class="fixed top-0 left-0 w-full h-16 bg-white">
      <div
        class="flex flex-nowrap h-full px-8 mx-auto border-b border-solid border-brand-gray-1"
      >
        <router-link
          to="/"
          class="flex items-center h-full text-xl"
        >
          新騎資訊
        </router-link>

        <nav class="h-full ml-12">
          <ul class="flex h-full p-0 m-0 list-none">
            <li
              v-for="menuItem in menuItems"
              :key="menuItem.text"
              data-test="main-nav-list-item"
              class="h-full ml-9 first:ml-0"
            >
              <router-link
                :to="menuItem.url"
                class="flex items-center h-full py-2.5"
                >{{ menuItem.text }}</router-link
              >
            </li>
          </ul>
        </nav>

        <div class="flex items-center h-full ml-auto">
          <profile-image
            v-if="isLogged"
            data-set="profile-image"
          />
          <action-button
            v-else
            data-set="login-button"
            text="hello"
            type="primary"
            @click="LOGIN_USER"
          />
        </div>
      </div>
      <subnav-menu v-if="isLogged" />
    </div>
  </header>
</template>

<script>
import { mapState, mapMutations } from "vuex";
import { LOGIN_USER } from "@/store";
import ActionButton from "../Shared/ActionButton.vue";
import ProfileImage from "./ProfileImage.vue";
import SubnavMenu from "./SubnavMenu.vue";
export default {
  name: "MainNav",
  components: {
    ActionButton,
    ProfileImage,
    SubnavMenu,
  },
  data() {
    return {
      menuItems: [
        { text: "Teams", url: "/" },
        { text: "Locations", url: "/" },
        { text: "Life at Bobo Corp", url: "/" },
        { text: "How we hire", url: "/" },
        { text: "Students", url: "/" },
        { text: "Jobs", url: "/jobs/results" },
      ],
    };
  },
  computed: {
    // isLogged() {
    //   return this.$store.state.isLogged;
    // },
    ...mapState(["isLogged"]),
    headerHeightClass() {
      return {
        "h-16": !this.isLogged,
        "h-32": this.isLogged,
      };
    },
  },
  methods: {
    // loggingUser() {
    //   this.$store.commit(LOGIN_USER);
    // },
    ...mapMutations([LOGIN_USER]),
  },
};
</script>
