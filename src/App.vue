<template>
  <v-app class="mt-0" id="app">
    <v-container grid-list-xl>
      <image-input v-model="avatar">
        <div slot="activator">
          <v-avatar class="grey lighten-3 mb-3" size="150px" v-ripple v-if="!avatar">
            <span>Click to add avatar</span>
          </v-avatar>
          <v-avatar class="mb-3" size="150px" v-ripple v-else>
            <img :src="avatar.imageURL" alt="avatar">
          </v-avatar>
        </div>
      </image-input>
      <v-slide-x-transition>
        <div v-if="avatar && saved == false">
          <v-btn class="primary" @click="uploadImage" :loading="saving">Save Avatar</v-btn>
        </div>
      </v-slide-x-transition>
    </v-container>
  </v-app>
</template>

<script>
import ImageInput from "./components/ImageInput.vue";

export default {
  name: "app",
  data() {
    return {
      avatar: null,
      saving: false,
      saved: false
    };
  },
  components: {
    ImageInput: ImageInput
  },
  watch: {
    avatar: {
      handler: function() {
        this.saved = false;
      },
      deep: true
    }
  },
  methods: {
    uploadImage() {
      this.saving = true;
      setTimeout(() => this.savedAvatar(), 1000);
    },
    savedAvatar() {
      this.saving = false;
      this.saved = true;
    }
  }
};
</script>
