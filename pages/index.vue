<template>
  <div>
    <div class="mt-5">
      <form @submit.prevent="onClickSearch">
        <v-row>
          <v-col>
            <v-text-field
              class="rounded-pill"
              required
              outlined
              label="Search"
              placeholder="Search"
              v-model="search_picture"
            >
              <template v-slot:append>
                <v-btn small icon type="submit">
                  <v-icon>mdi-image-search-outline</v-icon>
                </v-btn>
              </template>
            </v-text-field>
          </v-col>
        </v-row>
      </form>
    </div>

    <div>
      <v-row class="my-5">
        <v-col
          cols="4"
          class="d-flex child-flex"
          v-for="(item, index) in list_picture"
          :key="index"
        >
          <v-hover v-slot="{ hover }">
            <v-img class="rounded-lg" aspect-ratio="1" :src="item.src.medium">
              <template v-slot:placeholder>
                <v-row align="center" justify="center">
                  <v-progress-circular
                    indeterminate
                    color="grey lighten-5"
                  ></v-progress-circular>
                </v-row>
              </template>
              <v-expand-transition>
                <div
                  v-if="hover"
                  class="d-flex grey white--text v-card--reveal"
                >
                  <v-row class="px-2">
                    <v-col>
                      <h4>Photographer: {{ item.photographer }}</h4>
                    </v-col>
                  </v-row>
                </div>
              </v-expand-transition>
            </v-img>
          </v-hover>
        </v-col>
      </v-row>
    </div>
  </div>
</template>

<script>
export default {
  layout: "main",
  data() {
    return {
      search_picture: "",
      pexels_token: "563492ad6f9170000100000119f0b3a173d04a9b97c88161ca2746b0",
      list_picture: [],
    };
  },
  methods: {
    async onClickSearch() {
      await this.$axios
        .get("https://api.pexels.com/v1/search?query=" + this.search_picture, {
          headers: {
            Authorization: `Bearer ` + this.pexels_token,
            "Content-Type": "application/x-www-form-urlencoded",
          },
        })
        .then((response) => {
          this.list_picture = response.data.photos;
          console.log(response.data.photos);
        });
    },
  },
  watch: {
    async search_picture(item) {},
  },
};
</script>

<style>
.v-card--reveal {
  align-items: center;
  bottom: 0;
  justify-content: center;
  opacity: 0.5;
  position: absolute;
  width: 100%;
}
</style>