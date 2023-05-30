<template>
  <ion-app>
    <ion-router-outlet />
  </ion-app>
</template>

<script lang="ts" setup>
import { IonApp, IonRouterOutlet, useIonRouter } from "@ionic/vue";

import { store } from "./store";
import { supabase } from "./supabase";

const router = useIonRouter();

supabase.auth.onAuthStateChange(async (_, session) => {
  store.user = session?.user ?? {};
  if (session) {
    router.push("/account");
  } else {
    router.replace("/login");
  }
});
</script>
