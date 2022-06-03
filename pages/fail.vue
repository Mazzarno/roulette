<template>
  <vs-row justify="center" align="center" class="home">
    <vs-col w="12">
    <div class="video-responsive">
      <video
        autoplay
        webkit-playsinline="true"
        playsinline="true"
        controls
        class="video-mobile"
        src="@/assets/fail.mp4"
      ></video>
    </div>
    </vs-col>
    <vs-button to="/" size="xl" flat type="submit">
      Retour a l'accueil
    </vs-button>
  </vs-row>
</template>