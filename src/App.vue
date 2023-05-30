<template>
  <ion-app>
    <ion-router-outlet />
  </ion-app>
</template>

<script lang="ts">
import { IonApp, IonRouterOutlet, useIonRouter } from '@ionic/vue';
import { defineComponent, nextTick } from 'vue';

import { store } from './store';
import { supabase } from './supabase';

export default defineComponent({
  name: 'App',
  components: {
    IonApp,
    IonRouterOutlet
  },
  setup(){
    const router = useIonRouter();
    // supabase.auth.getUser().then(({data, error})=>{
    //   store.user = data?.user || {}
    // }, error => console.log(error));

    supabase.auth.onAuthStateChange(async (_, session) => {
      
      store.user = session?.user ?? {}
      if(session) {
        router.push('/account');
      } else {
        router.replace('/login');
      }
    })
  }
});
</script>
