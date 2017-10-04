<template>
  <div>
  <v-layout row wrap>
    <v-flex xs6>
      <div>
        <panel title="Song Metadata">
          <template slot="action">
          <v-btn  dark :to="{ name:'song-edit', params:{ songId : song.id}}" > Edit  </v-btn>
          </template>
          <v-layout>
            <v-flex xs12>
              <v-card class=" darken-3  mb-4">
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
                </v-container>
              </v-card>

            </v-flex>


          </v-layout>
        </panel>

      </div>
    </v-flex>
    <v-flex xs6 >
      <panel title="Youtube Video" class="ml-4">
        <youtube
                :video-id="song.youtubeId"
                :player-height="200"
                :player-width="550"
        ></youtube>

      </panel>
    </v-flex>
  </v-layout>
  <v-layout row wrap>
      <v-flex xs6>
        <div>
          <panel title="Song Lyrics">
            <v-text-field
                    box
                    readonly
                    multi-line
                    v-model="song.lyrics"
            >
              {{song.tab}}
            </v-text-field>
          </panel>

        </div>
      </v-flex>
      <v-flex xs6 >
        <panel title="Song Tab" class="ml-4">
          <v-text-field
                  box
                  readonly
                  multi-line
                  v-model="song.tab"
          >
            {{song.tab}}
          </v-text-field>
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
          id: this.$store.state.route.params.songId
        }
      }
    },
    components: {
      Panel
    },
    async mounted () {
      const songId = this.$store.state.route.params.songId
      this.song = (await SongsService.show(songId)).data
    }
  }
</script>
