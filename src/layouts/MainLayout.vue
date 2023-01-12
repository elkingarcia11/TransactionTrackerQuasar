<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated class="bg-secondary">
      <q-toolbar>
        <q-toolbar-title class="row justify-center toolbar-title">
          Transactions Tracker
        </q-toolbar-title>
        <q-btn
          size="md"
          flat
          icon-right="logout"
          color="white"
          label="Logout"
          id="logoutButton"
        />
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

export default defineComponent({
  name: 'MainLayout',

  setup() {
    const leftDrawerOpen = ref(false);

    return {
      leftDrawerOpen,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value;
      },
    };
  },
});
</script>
