<template>
  <v-app dark>
    <v-navigation-drawer
      v-model="drawer"
      :mini-variant="miniVariant"
      :clipped="clipped"
      fixed
      app
    >
      <v-list-item>
        <v-list-item-content>
          <v-list-item-title class="text-h5 font-weight-bold">
            <v-icon :x-large="!miniVariant">
              mdi-draw
            </v-icon> {{ title }}
          </v-list-item-title>
          <v-list-item-subtitle v-if="!miniVariant">
            Please keep social distancing!
          </v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>
      <v-divider />
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

      <v-btn
        fab
        small
        :style="{position:'fixed', top: [miniVariant ? 30 : 60] + 'px', right: '-15px'}"
        @click.stop="miniVariant = !miniVariant"
      >
        <v-icon>mdi-{{ `chevron-${miniVariant ? 'right' : 'left'}` }}</v-icon>
      </v-btn>
    </v-navigation-drawer>
    <v-app-bar
      class="appbarBgColor appbarColor--text"
      :clipped-left="clipped"
      fixed
      app
    >
      <v-spacer />
      <v-menu offset-y left>
        <template #activator="{ on, attrs }">
          <span
            v-bind="attrs"
            v-on="on"
          >
            Menu <v-icon dark>mdi-chevron-down</v-icon>
          </span>
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
      <!--
      <v-col cols="3" class="ml-n12">
        <v-autocomplete
          label="메뉴 이름을 검색해 보세요"
          class="mt-6"
          prepend-inner-icon="mdi-magnify"
        />
      </v-col>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      -->
      <v-avatar
        class="ml-3 mr-2"
        color="primary"
        size="40"
      >
        Yun
      </v-avatar>
      <span>
        Hi, <span class="font-weight-bold">Hose Yun</span>
      </span>
      <!--
      <v-btn
        icon
        @click.stop="rightDrawer = !rightDrawer"
      >
        <v-icon>mdi-menu</v-icon>
      </v-btn>
      -->
      <v-menu
        offset-x
        left
        :close-on-content-click="false"
      >
        <template #activator="{ on, attrs }">
          <v-btn
            fab
            small
            absolute
            bottom
            right
            v-bind="attrs"
            v-on="on"
          >
            <v-icon>mdi-cog</v-icon>
          </v-btn>
        </template>
        <v-list>
          <v-list-item>
            <v-list-item-title>
              <v-switch
                v-model="$vuetify.theme.dark"
                label="Dark Mode"
              />
            </v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>
    </v-app-bar>
    <v-main class="bgcolor">
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
    <v-snackbar
      v-model="snackbar"
      :timeout="timeout"
      :vertical="true"
      :centered="true"
    >
      {{ text }}

      <template #action="{ attrs }">
        <v-btn
          color="blue"
          text
          v-bind="attrs"
          @click="snackbar = false"
        >
          닫기
        </v-btn>
      </template>
    </v-snackbar>
  </v-app>
</template>

<script>
export default {
  data () {
    return {
      clipped: false,
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
          title: '경비 신청(Stepper,Vertical)',
          to: '/expense-stepper-v'
        },
        {
          icon: 'mdi-chart-bubble',
          title: '경비 신청(Stepper,Horizontal)',
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
      title: 'SIGN WEB',
      snackbar: false,
      text: 'My timeout is set to 2000.',
      timeout: 2000
    }
  },
  created () {
    this.$nuxt.$on('onSnackBar', (text, timeout) => {
      this.text = text
      this.snackbar = true
      if (!timeout) {
        this.timeout = 0
      }
    })
  }
}
</script>
