<template>
  <v-container
    fluid
    grid-list-xs
    :class="$vuetify.breakpoint.xs ? 'fillPad' : ''"
  >
    <v-row
      justify="center"
      class="mt-16 py-6 hidden-xs-only"
      :class="$vuetify.breakpoint.xs ? '' : 'ml-5'"
    >
      <v-row justify="space-around">
        <v-btn color="black" dark large><h1>GAMING</h1></v-btn>
        <div class="d-inline-flex">
          <v-icon large color="white">mdi-timer</v-icon>
          <v-card
            width="70px"
            v-for="(item, i) in times"
            :key="i"
            class="text-center py-2 mx-1"
          >
            <h2>{{ item.time }}{{ item.text }}</h2>
            <v-divider></v-divider>
          </v-card>
        </div>
      </v-row>
    </v-row>
    <v-row justify="center" class="hidden-sm-and-up">
      <v-btn label color="black" dark large><h1>GAMING</h1></v-btn>
    </v-row>
    <v-row justify="end" class="hidden-xs-only pr-16">
      <v-col cols="10" md="11">
        <v-sheet
          class="mx-auto roundedCard"
          color="sheetBg"
          elevation="8"
          height="62vh"
        >
          <v-slide-group
            class="pa-4"
            prev-icon="mdi-gamepad-round-left"
            next-icon="mdi-gamepad-round-right"
            selected-class="bg-primary"
            show-arrows
          >
            <v-slide-item v-for="(item, i) in merchItems" :key="'A' + i">
              <v-card
                class="roundedCard cardBgPurple text-center pointer mx-3 mt-16"
                height="450"
                width="350"
              >
                <v-img
                  class="align-end text-white imageEffect"
                  height="500px"
                  :src="require('@/assets/' + item.src)"
                  contain
                >
                </v-img>
                <h3 class="textEffect2 mt-2">{{ item.title }}</h3>
                <h1 class="textEffect2">{{ item.price }}</h1>
                <v-card-actions>
                  <v-row justify="center">
                    <v-col cols="5">
                      <v-btn
                        block
                        class="btnBgPurple textEffect2 white--text"
                        :href="item.link"
                        target="_blank"
                      >
                        BUY NOW
                      </v-btn></v-col
                    ></v-row
                  >
                </v-card-actions>
              </v-card>
            </v-slide-item>
          </v-slide-group>
        </v-sheet>
      </v-col>
    </v-row>
    <v-row justify="center" class="mt-7 pb-2 hidden-xs-only">
      <v-col cols="10" sm="9" class="ml-16">
        ><v-btn label color="black" dark large
          ><h1>VIMNITE MERCH</h1></v-btn
        ></v-col
      >
    </v-row>

    <v-row justify="end" class="hidden-xs-only pr-16">
      <v-col cols="10" md="11">
        <v-sheet
          class="mx-auto roundedCard"
          color="sheetBg"
          elevation="8"
          height="62vh"
        >
          <v-slide-group
            class="pa-4"
            prev-icon="mdi-gamepad-round-left"
            next-icon="mdi-gamepad-round-right"
            selected-class="bg-primary"
            show-arrows
          >
            <v-slide-item v-for="(item, i) in scheduledMerch" :key="'B' + i">
              <v-card
                class="roundedCard cardBgPurple text-center pointer mx-3 mt-16"
                height="450"
                width="350"
              >
                <v-img
                  class="align-end text-white imageEffect"
                  height="500px"
                  :src="item.merchPhoto"
                  contain
                >
                </v-img>
                <h3 class="textEffect2 mt-2">{{ item.title }}</h3>
                <h1 class="textEffect2">${{ item.price }}</h1>
                <v-card-actions>
                  <v-row justify="center">
                    <v-col cols="5">
                      <v-btn
                        block
                        class="btnBgPurple textEffect2 white--text"
                        :href="item.link"
                        target="_blank"
                      >
                        BUY NOW
                      </v-btn></v-col
                    ></v-row
                  >
                </v-card-actions>
              </v-card>
            </v-slide-item>
          </v-slide-group>
        </v-sheet>
      </v-col>
    </v-row>
    <v-row justify="center" class="hidden-sm-and-up pb-16">
      <v-card
        class="roundedCard cardBgPurple text-center pointer mx-3 mt-16 mb-10"
        height="450"
        width="350"
        v-for="(item, i) in merchItems"
        :key="'B' + i"
      >
        <v-img
          class="align-end text-white imageEffect"
          height="500px"
          :src="require('@/assets/' + item.src)"
          contain
        >
        </v-img>
        <h3 class="textEffect2 mt-2">{{ item.title }}</h3>
        <h1 class="textEffect2">{{ item.price }}</h1>
        <v-card-actions>
          <v-row justify="center">
            <v-col cols="5">
              <v-btn
                block
                class="btnBgPurple textEffect2 white--text"
                :href="item.link"
                target="_blank"
              >
                BUY NOW
              </v-btn></v-col
            ></v-row
          >
        </v-card-actions>
      </v-card>
    </v-row>
    <v-row justify="center" class="hidden-sm-and-up">
      <v-btn label color="black" dark large><h1>VIMNITE</h1></v-btn>
    </v-row>
  </v-container>
</template>
<script>
import { mapState, mapActions } from "vuex";
export default {
  name: "StoreView",
  components: {},

  computed: {
    ...mapState(["store", "scheduledMerch"]),
  },

  data() {
    return {
      startTime: "April 2, 2023 12:00:00",
      endTime: "April 30, 2023 12:00:00",
      model: null,
      times: [
        { id: 0, text: "D", time: 1 },
        { id: 1, text: "H", time: 1 },
        { id: 2, text: "M", time: 1 },
        { id: 3, text: "S", time: 1 },
      ],
      merchItems: [
        {
          src: "merchLaunch/tshirtKBMGang.png",
          title: "KBM GANG - TSHIRT",
          price: "$30",
          link: "https://vimnite-shop.fourthwall.com/products/vforce-kbm-gang",
        },
        {
          src: "merchLaunch/tshirtControllerGang.png",
          title: "CONTROLLER GANG - TSHIRT",
          price: "$30",
          link: "https://vimnite-shop.fourthwall.com/products/vforce-controller-gang",
        },
        {
          src: "merchLaunch/tshirtMyLucky.png",
          title: "MY LUCKY GAMING - TSHIRT",
          price: "$30",
          link: "https://vimnite-shop.fourthwall.com/products/vforce-my-lucky-tshirt",
        },
        {
          src: "merchLaunch/tshirtMySquadIsBetter.png",
          title: "MY SQUAD IS BETTER - TSHIRT",
          price: "$30",
          link: "https://vimnite-shop.fourthwall.com/products/my-squad-is-better",
        },
        {
          src: "merchLaunch/tshirtLateNightGamer.png",
          title: "LATE NIGHT GAMER - TSHIRT",
          price: "$30",
          link: "https://vimnite-shop.fourthwall.com/products/vforce-late-night-gamer",
        },
      ],
      progress: 100,
      timeinterval: undefined,
    };
  },
  created() {
    this.updateTimer();
    this.timeinterval = setInterval(this.updateTimer, 1000);
    this.GET_SCHEDULED_MERCH();
  },
  methods: {
    ...mapActions(["GET_SCHEDULED_MERCH"]),
    updateTimer() {
      if (
        this.times[3].time > 0 ||
        this.times[2].time > 0 ||
        this.times[1].time > 0 ||
        this.times[0].time > 0
      ) {
        this.getTimeRemaining();
        this.updateProgressBar();
      } else {
        clearTimeout(this.timeinterval);
        // this.times[3].time = this.times[2].time = this.times[1].time = this.times[0].time = 0;
        this.progress = 0;
      }
    },
    getTimeRemaining() {
      let t = Date.parse(new Date(this.endTime)) - Date.parse(new Date());
      if (t >= 0) {
        this.times[3].time = Math.floor((t / 1000) % 60); //seconds
        this.times[2].time = Math.floor((t / 1000 / 60) % 60); //minutes
        this.times[1].time = Math.floor((t / (1000 * 60 * 60)) % 24); //hours
        this.times[0].time = Math.floor(t / (1000 * 60 * 60 * 24)); //days
      } else {
        this.times[3].time =
          this.times[2].time =
          this.times[1].time =
          this.times[0].time =
            0;
        this.progress = 0;
      }
    },
    updateProgressBar() {
      let startTime = Date.parse(new Date(this.startTime));
      let currentTime = Date.parse(new Date());
      let endTime = Date.parse(new Date(this.endTime));
      let interval = parseFloat(
        ((currentTime - startTime) / (endTime - startTime)) * 100
      ).toFixed(2);
      this.progress = 100 - interval;
    },
  },
};
</script>
<style>
.v-icon.notranslate.mdi.mdi-gamepad-round-right.theme--light {
  color: white !important;
  font-size: 50px;
  padding-left: 20px;
}
.v-icon.notranslate.mdi.mdi-gamepad-round-left.theme--light {
  color: white !important;
  font-size: 50px;
}

.cardBgPurple {
  background-color: #ffdee9;
  background-image: linear-gradient(0deg, #ffdee9 0%, #b5fffc 100%);
}
.btnBgPurple {
  background-image: linear-gradient(
    109.2deg,
    rgba(107, 52, 255, 1) 16.5%,
    rgb(0, 120, 218) 81%
  );
}

.imageEffect {
  position: relative;
  top: -130px;
}

.textEffect2 {
  position: relative;
  top: -200px;
}
.fillPad {
  padding-bottom: 145px;
}
</style>
