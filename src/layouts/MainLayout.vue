<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated class="bg-secondary">
      <q-toolbar>
        <q-toolbar-title>
          <q-btn
            flat
            icon="receipt_long"
            size="lg"
            label="Transactions Tracker"
          />
        </q-toolbar-title>
        <template v-if="isNotLogin()">
          <q-btn
            v-if="$q.platform.is.mobile"
            size="md"
            flat
            icon="logout"
            color="white"
            id="logoutButton"
          />
          <q-btn
            v-else
            size="md"
            flat
            icon-right="logout"
            color="white"
            label="Logout"
            id="logoutButton"
          />
        </template>
      </q-toolbar>
    </q-header>

    <q-page-container class="bg-primary">
      <router-view />
    </q-page-container>

    <q-footer class="text-black footer">
      <q-toolbar>
        <q-toolbar-title class="row items-center q-px-sm q-py-md">
          <q-avatar>
            <img src="../assets/logo.png" />
          </q-avatar>
          <div class="q-pl-md footer-title">Embarque Tenares Corp. © 1998</div>
        </q-toolbar-title>
      </q-toolbar>
    </q-footer>
  </q-layout>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import { useQuasar } from 'quasar';
export default defineComponent({
  name: 'MainLayout',
  methods: {
    isNotLogin() {
      if (this.$route.path != '/') {
        return true;
      } else {
        return false;
      }
    },
  },
  setup() {
    const leftDrawerOpen = ref(false);

    const $q = useQuasar();
    $q.platform.is.mobile;
    return {
      leftDrawerOpen,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value;
      },
    };
  },
});
</script>
