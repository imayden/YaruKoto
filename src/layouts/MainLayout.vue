<template>
  <q-layout view="lHh Lpr lFf">
    <!-- Header with shade -->
    <!-- <q-header elevated> -->
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />
        <!-- <q-toolbar-title> -->
          <!-- Quasar App -->
        <!-- </q-toolbar-title> -->
        <!-- <div>Quasar v{{ $q.version }}</div> -->
      </q-toolbar>

      <div class="q-px-lg q-pt-xl q-mb-md">
        <div class="text-h3">YaruKoto</div>
        <div class="text-subtitle1">
          {{todaysDate}}
        </div>
      </div>

      <q-img
        src="/src/statics/header.jpg"
        class="header-image absolute-top"
        />

    </q-header>

    <!-- Drawer content -->
    <q-drawer
        v-model="leftDrawerOpen"
        show-if-above
        :width="250"
        :breakpoint="600"
        class="column" :style="{ backgroundColor: '#F9F4EB' }"
        elevated
      >
        <q-scroll-area style="height: calc(100% - 192px); margin-top: 192px; border-right: 1px solid #F9F4EB">
          <q-list padding>

            <!-- Homepage: YaruKoto -->
            <q-item
              to="/"
              exact
              clickable
              v-ripple>
              <!-- Icon -->
              <q-item-section avatar>
                <q-icon name="today"/>
              </q-item-section>
              <!-- Text -->
              <q-item-section>
                YaruKoto
              </q-item-section>
            </q-item>

            <!-- Guide -->
            <q-item
              to="guide"
              exact
              clickable
              v-ripple>
              <!-- Icon -->
              <q-item-section avatar>
                <q-icon name="flag" />
              </q-item-section>
              <!-- Text -->
              <q-item-section>
                Guide
              </q-item-section>
            </q-item>

            <!-- <q-item active clickable v-ripple>
              <q-item-section avatar>
                <q-icon name="star" />
              </q-item-section>

              <q-item-section>
                Star
              </q-item-section>
            </q-item> -->
          </q-list>
        </q-scroll-area>

        <q-img
          class="absolute-top"
          src="src/statics/a-header.jpg"
          style="height: 192px" >
          <div class="absolute-bottom bg-transparent">

            <!-- Avatar -->
            <q-avatar size="56px" class="q-mb-sm">
              <img src="src/statics/avatar.jpg">
            </q-avatar>

            <!-- User Name -->
            <div class="text-weight-bold">Ayden Deng</div>
            <div>@imayden_com</div>
          </div>
        </q-img>
      </q-drawer>

    <q-page-container>
      <keep-alive>
        <router-view />
      </keep-alive>
    </q-page-container>
  </q-layout>
</template>

<script>
import { date } from 'quasar'
import { defineComponent, ref } from 'vue'
import EssentialLink from 'components/EssentialLink.vue'

const linksList = [
  {
    title: 'Docs',
    caption: 'quasar.dev',
    icon: 'school',
    link: 'https://quasar.dev'
  },
  {
    title: 'Github',
    caption: 'github.com/quasarframework',
    icon: 'code',
    link: 'https://github.com/quasarframework'
  },
  {
    title: 'Discord Chat Channel',
    caption: 'chat.quasar.dev',
    icon: 'chat',
    link: 'https://chat.quasar.dev'
  },
  {
    title: 'Forum',
    caption: 'forum.quasar.dev',
    icon: 'record_voice_over',
    link: 'https://forum.quasar.dev'
  },
  {
    title: 'Twitter',
    caption: '@quasarframework',
    icon: 'rss_feed',
    link: 'https://twitter.quasar.dev'
  },
  {
    title: 'Facebook',
    caption: '@QuasarFramework',
    icon: 'public',
    link: 'https://facebook.quasar.dev'
  },
  {
    title: 'Quasar Awesome',
    caption: 'Community Quasar projects',
    icon: 'favorite',
    link: 'https://awesome.quasar.dev'
  }
]

export default defineComponent({
  name: 'MainLayout',

  components: {
    EssentialLink
  },

  setup () {
    const leftDrawerOpen = ref(false)

    return {
      essentialLinks: linksList,
      leftDrawerOpen,
      toggleLeftDrawer () {
        leftDrawerOpen.value = !leftDrawerOpen.value
      }
    }
  },

  computed: {
    todaysDate() {
      // manipulate dates
      const timeStamp = Date.now();
      return date.formatDate(timeStamp, 'ddd · Week w | MMM Do · YYYY');
    }
  }
})
</script>

<style lang="scss">
  .header-image{
    height: 100%;
    z-index: -1;
    opacity:0.10;
    filter: grayscale(100%);
  }
</style>
