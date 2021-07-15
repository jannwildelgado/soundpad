/* eslint-disable vue/no-parsing-error */
<template>
  <v-app>
    <v-main>
      <v-container fill-height>
        <div class="page">
          <v-card
            elevation="0"
            outlined
            class="max-auto"
          >
            <v-card-text>
              <v-btn
                v-for="(sound, key) of soundList"
                :key="key"
                class="ma-2"
                :class="[
                  {'on-active':currPlaying === sound}
                ]"
                color="secondary"
                elevation="2"
                @click="initSounds(sound)"
                :dark="currPlaying === sound"
              >
                <v-icon
                  v-if="currPlaying === sound"
                  class="mr-2"
                >
                  mdi-volume-high
                </v-icon>

                {{ sound }}
              </v-btn>
            </v-card-text>
          </v-card>
        </div>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import { Howl } from 'howler'

export default {
  name: 'SoundPad',

  components: {},

  data: () => ({
    id: null,
    sound: null,
    currPlaying: '',
    soundList: [
      'sound1',
      'sound2',
      'sound3',
      'sound4',
      'sound5',
      'sound6',
      'sound7',
      'sound8',
      'sound9'
    ]
  }),

  created () {},

  mounted () {
    document.title = 'SoundPad'
  },

  methods: {
    initSounds (sound) {
      if (this.id) {
        this.sound.stop(this.id)
      }

      const path = require(`./assets/sounds/${sound}.mp3`)

      this.sound = new Howl({
        src: [path],
        autoplay: false,
        loop: false,
        volume: 1,
        onplay: () => {
          this.currPlaying = sound
          console.log('Now playing...')
        },
        onend: () => {
          this.currPlaying = ''
          console.log('Finished!')
        }
      })

      this.id = this.sound.play()
    }
  }
};
</script>

<style lang="css" scoped>
.page {
  height: 100%;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.on-active {
  background-image: linear-gradient(to right, #84fab0 0%, #8fd3f4 51%, #84fab0 100%);
}
</style>