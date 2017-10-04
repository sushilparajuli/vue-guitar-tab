<template>
  <div class="hello">
    <v-layout column>
      <v-flex xs6 offset-xs3>
        <panel title="Songs">
          <router-link
                  slot="action"
                  :to="{ name: 'songs-create'}">
            <v-btn

                    class=" accent-2"
                    light
                    medium
                    absolute
                    success
                    middle
                    fab>
              <v-icon>add</v-icon>
            </v-btn>
          </router-link>
          <div
                  v-for="song in songs"
                  :key="song.title">
            <v-layout>
              <v-flex xs12>
                <v-card class="blue-grey darken-3 white--text mb-4">
                  <v-container fluid grid-list-lg>
                    <v-layout row>
                      <v-flex xs7>
                        <div>
                          <div class="headline">{{song.title}}</div>
                          <div>{{song.artist}}</div>
                          <div>{{song.album}}</div>
                          <v-chip>{{song.genre}}</v-chip>
                        </div>
                      </v-flex>
                      <v-flex xs5>
                        <v-card-media
                                :src="song.albumImageUrl"
                                height="125px"
                                contain
                        ></v-card-media>
                      </v-flex>

                    </v-layout>
                    <v-layout row>
                      <v-btn block light :to="{ name:'song', params:{ songId : song.id}}"> Details</v-btn>
                    </v-layout>
                  </v-container>
                </v-card>

              </v-flex>

            </v-layout>

          </div>
        </panel>
      </v-flex>
    </v-layout>

  </div>
</template>

<script>
  import SongsService from '@/services/SongsService'
  import Panel from '@/components/Panel'
  export default {
    name: 'songs',
    components: {
      Panel
    },
    data () {
      return {
        songs: null
      }
    },
    async mounted () {
      this.songs = (await SongsService.index()).data
    }
  }
</script>

