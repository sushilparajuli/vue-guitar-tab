<template>
  <div>
    <v-layout>
      <v-flex xs4>
        <panel title="Song Metadata">
          <v-text-field
                  label="Title"
                  v-model="song.title"
                  :rules="[rules.required]"
          ></v-text-field>

          <v-text-field
                  label="Artist"
                  v-model="song.artist"
                  :rules="[rules.required]"
          ></v-text-field>

          <v-text-field
                  label="Genre"
                  v-model="song.genre"
                  :rules="[rules.required]"
          ></v-text-field>

          <v-text-field
                  label="Album"
                  v-model="song.album"
                  :rules="[rules.required]"
          ></v-text-field>

          <v-text-field
                  label="Album Image Url"
                  v-model="song.albumImageUrl"
                  :rules="[rules.required]"
          ></v-text-field>

          <v-text-field
                  label="Youtube Id"
                  v-model="song.youtubeId"
                  :rules="[rules.required]"
          ></v-text-field>

        </panel>
      </v-flex>

      <v-flex xs8>
        <panel title="Song Structure" class="ml-4">
          <v-text-field
                  label="Lyrics"
                  v-model="song.lyrics"
                  :rules="[rules.required]"
                  multi-line
          ></v-text-field>

          <v-text-field
                  label="Tab"
                  v-model="song.tab"
                  :rules="[rules.required]"
                  multi-line
          ></v-text-field>
          <v-alert
                  error
                  value="true"
                  v-if="error"
                  transition="scale-transition"
          >
            {{error}}
          </v-alert>
          <v-btn
                  success
                  dark
                  type="submit" @click="create"> Create Song
          </v-btn>
        </panel>



      </v-flex>
    </v-layout>
  </div>
</template>

<script>
  import Panel from '@/components/Panel'
  import SongsService from '@/services/SongsService'
  export default{
    data () {
      return {
        song: {
          title: null,
          artist: null,
          genre: null,
          album: null,
          albumImageUrl: null,
          youtubeId: null,
          lyrics: null,
          tab: null
        },
        error: null,
        rules: {
          required: (value) => !!value || 'Required.'
        }
      }
    },
    components: {
      Panel
    },
    methods: {
      async create () {
        this.error = null
        const areAllFieldsFilledIn = Object
          .keys(this.song)
          .every(key => !!this.song[key])
        if (!areAllFieldsFilledIn) {
          this.error = 'Please fill in the required fields'
          return
        }
        try {
          await SongsService.post(this.song)
          this.$router.push({
            name: 'songs'
          })
        } catch (err) {
          console.log(err)
        }
      }
    }
  }
</script>
