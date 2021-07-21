<template>
  <v-app dark>
    <v-navigation-drawer
      v-model="drawer"
      :mini-variant="miniVariant"
      :clipped="clipped"
      fixed
      app
    >
      <v-list>
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
        >
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="item.title" />
          </v-list-item-content>
        </v-list-item>
      </v-list>

      <template #append>
        <div class="pa-2">
          <v-btn block>
            Logout
          </v-btn>
        </div>
      </template>
    </v-navigation-drawer>
    <v-app-bar
      :clipped-left="clipped"
      fixed
      app
    >
      <v-col cols="1">
        <v-toolbar-title class="text-h5 font-weight-bold" v-text="title" />
      </v-col>
      <v-col cols="1">
        <v-menu offset-y>
          <template #activator="{ on, attrs }">
            <a
              class="white--text"
              v-bind="attrs"
              v-on="on"
            >
              신청메뉴 <v-icon>mdi-chevron-down</v-icon>
            </a>
          </template>
          <v-list>
            <v-list-item
              v-for="(item, index) in items"
              :key="index"
            >
              <v-list-item-title>{{ item.title }}</v-list-item-title>
            </v-list-item>
          </v-list>
        </v-menu>
      </v-col>
      <v-col cols="3" class="ml-n12">
        <v-autocomplete
          label="메뉴 이름을 검색해 보세요"
          class="mt-6"
          prepend-inner-icon="mdi-magnify"
        />
      </v-col>
      <v-spacer />
      <v-spacer />
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-btn
        icon
        @click.stop="miniVariant = !miniVariant"
      >
        <v-icon>mdi-{{ `chevron-${miniVariant ? 'right' : 'left'}` }}</v-icon>
      </v-btn>
      <v-btn
        icon
        @click="$vuetify.theme.dark=!$vuetify.theme.dark"
      >
        <v-icon>mdi-theme-light-dark</v-icon>
      </v-btn>
      <!--
      <v-btn
        icon
        @click.stop="rightDrawer = !rightDrawer"
      >
        <v-icon>mdi-menu</v-icon>
      </v-btn>
      -->
    </v-app-bar>
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
    <v-navigation-drawer
      v-model="rightDrawer"
      :right="right"
      temporary
      fixed
    >
      <v-list>
        <v-list-item @click.native="right = !right">
          <v-list-item-action>
            <v-icon light>
              mdi-repeat
            </v-icon>
          </v-list-item-action>
          <v-list-item-title>Switch drawer (click me)</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-footer
      app
      :absolute="true"
    >
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data () {
    return {
      clipped: true,
      drawer: false,
      items: [
        {
          icon: 'mdi-apps',
          title: 'Welcome',
          to: '/'
        },
        {
          icon: 'mdi-chart-bubble',
          title: '경비 신청',
          to: '/expense'
        },
        {
          icon: 'mdi-chart-bubble',
          title: '경비 신청(Stepper)',
          to: '/expense-stepper'
        },
        {
          icon: 'mdi-chart-bubble',
          title: '예약 시스템',
          to: '/calendar'
        },
        {
          icon: 'mdi-chart-bubble',
          title: '예약 시스템2',
          to: '/calendar2'
        }
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: '전자결재'
    }
  }
}
</script>
