<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar class="q-py-xl justify-between">
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />
        <div class="text-h4">Unicorn party</div>
        <div class="text-right">{{ unicornDate }}</div>
      </q-toolbar>
      <q-img
        class="backround_unicorn absolute-top"
        src="../assets/unicorn.jpg"
      ></q-img>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      :width="250"
      :breakpoint="600"
    >
      <q-scroll-area
        style="
          height: calc(100% - 136px);
          margin-top: 136px;
          border-right: 1px solid #ddd;
        "
      >
        <q-list padding>
          <!-- to="/" exact так мы прописываем наш путь к страничкам -->
          <q-item to="/" exact clickable v-ripple>
            <q-item-section avatar>
              <q-icon name="list" />
            </q-item-section>

            <q-item-section> Todo </q-item-section>
          </q-item>

          <q-item to="/help" exact clickable v-ripple>
            <q-item-section avatar>
              <q-icon name="help" />
            </q-item-section>

            <q-item-section> Help </q-item-section>
          </q-item>

          <q-item to="/about" exact clickable v-ripple>
            <q-item-section avatar>
              <q-icon name="groups" />
            </q-item-section>

            <q-item-section> About us </q-item-section>
          </q-item>

          <q-item to="/contacts" exact clickable v-ripple>
            <q-item-section avatar>
              <q-icon name="contact_phone" />
            </q-item-section>

            <q-item-section> Contacts </q-item-section>
          </q-item>
        </q-list>
      </q-scroll-area>

      <q-img class="absolute-top q-drawer-bacground" style="height: 136px">
        <div class="absolute-bottom bg-transparent">
          <q-avatar size="56px" class="q-mb-sm">
            <img src="..\assets\unicorn_avatar.jpg" />
          </q-avatar>
          <div class="text-weight-bold">Ekaterina Pavlova</div>
          <div>@chiki-riki</div>
        </div>
      </q-img>
    </q-drawer>

    <q-page-container>
      <!-- keep нам помогает в том, чтобы при переключении между страничками наши динамические данные не пропадали -->
      <keep-alive>
        <router-view />
      </keep-alive>
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent, ref } from "vue";
import EssentialLink from "components/EssentialLink.vue";
import { date } from "quasar";

const linksList = [
  {
    title: "Docs",
    caption: "quasar.dev",
    icon: "school",
    link: "https://quasar.dev",
  },
  {
    title: "Github",
    caption: "github.com/quasarframework",
    icon: "code",
    link: "https://github.com/quasarframework",
  },
  {
    title: "Discord Chat Channel",
    caption: "chat.quasar.dev",
    icon: "chat",
    link: "https://chat.quasar.dev",
  },
  {
    title: "Forum",
    caption: "forum.quasar.dev",
    icon: "record_voice_over",
    link: "https://forum.quasar.dev",
  },
  {
    title: "Twitter",
    caption: "@quasarframework",
    icon: "rss_feed",
    link: "https://twitter.quasar.dev",
  },
  {
    title: "Facebook",
    caption: "@QuasarFramework",
    icon: "public",
    link: "https://facebook.quasar.dev",
  },
  {
    title: "Quasar Awesome",
    caption: "Community Quasar projects",
    icon: "favorite",
    link: "https://awesome.quasar.dev",
  },
];

export default defineComponent({
  name: "MainLayout",

  components: {
    EssentialLink,
  },
  setup() {
    const leftDrawerOpen = ref(false);

    return {
      essentialLinks: linksList,
      leftDrawerOpen,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value;
      },
    };
  },
  computed: {
    unicornDate() {
      const timeStamp = Date.now();
      return date.formatDate(timeStamp, "dddd DD.MM.YYYY");
    },
  },
});
</script>

<style>
.backround_unicorn {
  opacity: 0.2;
  height: 100%;
  z-index: -1;
}

.q-drawer-bacground {
  background: #e069b9;
}
</style>
