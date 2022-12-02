<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Editar Perfil</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Editar Perfil</ion-title>
        </ion-toolbar>
      </ion-header>

      <ion-list>
        <ion-item>
          <ion-label>Foto de Perfil</ion-label>
          <ion-input
            :value="user.imagem"
            @ionInput="user.imagem = $event.target.value"
          ></ion-input>
        </ion-item>

        <ion-item>
          <ion-label>Nome de Usuario</ion-label>
          <ion-input
            :value="user.nome"
            @ionInput="user.nome = $event.target.value"
          ></ion-input>
        </ion-item>

        <ion-item>
          <h2>Biografia</h2>
        </ion-item>

        <ion-item>
          <ion-textarea
            :value="user.bio"
            @ionInput="user.bio = $event.target.value"
            placeholder="Digite aqui a nova biografia.."
          ></ion-textarea>
        </ion-item>
      </ion-list>
    </ion-content>
    <ion-footer>
      <ion-button expand="full" @click="sendData">Editar</ion-button>
    </ion-footer>
  </ion-page>
</template>

<script lang="ts">
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
} from "@ionic/vue";

import { ref } from "vue";
import axios from "axios";

export default {
  name: "Tab2",
  components: { IonHeader, IonToolbar, IonTitle, IonContent, IonPage },
  setup() {
    const user = ref({
      imagem: `https://static.wikia.nocookie.net/horadeaventurabr/images/c/cd/Jake999.png/revision/latest?cb=20130407021850&path-prefix=pt-br`,
      nome: `a`,
      bio: `b`,
    });

    function sendData() {
      axios.put(`https://app-perfil-d19a2-default-rtdb.firebaseio.com/.json`, {
        user: {
          ...user.value,
        },
      });
    }

    return {
      user,
      sendData,
    };
  },
};
</script>

<style scoped>
</style>