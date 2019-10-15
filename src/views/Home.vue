<template>
  <div class="views Home">
    <div v-if="phase === 0">
      <h1 class="title">Voice 2 Meme</h1>
      <img class="mouthImg" src="@/assets/images/mouth.png" />
      <button @click="speakYourMeme">Speak Your Meme!</button>
    </div>
    <h3 v-if="!hasMemed">
      <v-icon class="icon-alert">mdi-alert</v-icon>
      <br />
      Works best on Chrome, may not work on iPhone iOS!
    </h3>
    <img class="memeImg" :src="imgSrc" v-if="imgSrc" />
    <v-progress-circular class="progress-circular" indeterminate v-if="hasMemed && !imgSrc"></v-progress-circular>
  </div>
</template>

<style lang="scss" scoped>
@import "@/main.scss";

.Home {
  .title {
    margin-bottom: 50px;
    font-size: 50px;
    text-shadow: 0 1px 0 $appBlack, 0 2px 8px lighten($appWhite, 25%);
  }

  .mouthImg {
    display: block;
    margin: auto;
    margin-bottom: 70px;
  }

  button {
    display: block;
    margin: auto;
    margin-bottom: 24px;
    width: 90%;
    max-width: 300px;
    background-color: $appWhite;
    color: $appBlack;
    border: 1px solid $appBlack;
    box-shadow: 0 2px 16px lighten($appWhite, 50%);
  }

  .icon-alert {
    color: $appAlert;
  }

  .progress-circular {
    color: $appWhite;
  }

  .memeImg {
    width: 33%;
  }
}
</style>

<script>
export default {
  name: "Home",
  data() {
    return {
      phase: 0,

      hasMemed: false,
      imgSrc: ""
    };
  },
  methods: {
    speakYourMeme() {
      this.hasMemed = true;

      const recognition = window.SpeechRecognition
        ? new SpeechRecognition()
        : new webkitSpeechRecognition();

      recognition.start();
      recognition.onresult = event => {
        const result = event.results[0][0].transcript;
        const splitResult = result.split(" ");
        const topText = splitResult
          .slice(0, Math.floor(splitResult.length / 2))
          .join(" ");
        const bottomText = splitResult
          .slice(Math.floor(splitResult.length / 2))
          .join(" ");

        // console.log(topText, bottomText);

        this.imgSrc = `https://memegen.link/buzz/${topText}/${bottomText}.jpg`;
      };
    }
  }
};
</script>
