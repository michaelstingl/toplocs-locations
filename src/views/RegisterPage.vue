<template>
  <ion-page class="ion-text-center">
    <form
      ref="form"
      @submit.prevent="onSubmit"
    >
      <div class="logo-container">
        <ion-img
          src="/assets/logo.png"
          alt="App Logo"
          class="logo"
        />
      </div>
      <ion-list class="ion-margin-top">
        <ion-list-header class="ion-margin-top">
          <ion-title>
            Create an account or <a href="/login" target="_self">Login</a>
          </ion-title>
        </ion-list-header>

        <ion-item v-if="errorMessage" class="ion-margin-bottom" lines="none">
           {{ errorMessage }}
        </ion-item>

        <ion-item class="ion-margin-bottom" lines="none">
          <ion-input
            name="username"
            type="text"
            label="Username"
            labelPlacement="fixed"
            fill="outline"
          ></ion-input>
        </ion-item>

        <ion-item class="ion-margin-bottom" lines="none">
          <ion-input
            name="email"
            type="email"
            label="Email"
            labelPlacement="fixed"
            fill="outline"
          ></ion-input>
        </ion-item>

        <ion-item class="ion-margin-bottom" lines="none">
          <ion-input
            name="password"
            type="password"
            label="Password"
            labelPlacement="fixed"
            fill="outline"
          ></ion-input>
        </ion-item>

        <ion-item class="ion-margin-bottom" lines="none">
          <ion-input
            name="password2"
            type="password"
            label="Confirm Password"
            labelPlacement="fixed"
            fill="outline"
          ></ion-input>
        </ion-item>

        <ion-button
          class="ion-padding"
          type="submit"
          shape="round"
          expand="full"
        > Sign Up
        </ion-button>
      </ion-list>
    </form>

  </ion-page>
</template>

<script setup lang="ts">
  import { ref } from 'vue';
  import { useRouter } from 'vue-router';
  import {
    IonList,
    IonItem,
    IonListHeader,
    IonInput,
    IonPage,
    IonButton,
    IonTitle,
    IonImg,
  } from '@ionic/vue';
  import { reloadSession } from '@/services/sessionService';
  import { useUser } from '@/composables/user';

  const { register } = useUser();
  const router = useRouter();
  const errorMessage = ref('');
  const form = ref<HTMLFormElement | null>(null);

  const onSubmit = async () => {
    if (!form.value) return;
    errorMessage.value = '';
    try {
      const formData = new FormData(form.value ?? undefined);
      const response = await register(formData);
      await reloadSession();

      if (response) router.push('/tabs');
    } catch (error) {
      errorMessage.value = (error as any).response?.data || 'An error occurred';
      console.error(error);
    }
  }
</script>

<style scoped>
  .logo-container {
    display: flex;
    justify-content: center;
    margin-top: 100px;
  }

  .logo {
    width: 120px;
    height: auto;
  }
</style>