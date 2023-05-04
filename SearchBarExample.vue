<template>
  <div class="text-center mt-4">
    <v-menu
      v-model="menu"
      :close-on-click="false"
      :close-on-content-click="false"
      :open-on-click="false"
      offset-y
    >
      <template v-slot:activator="{ on }">
        <v-text-field
          label="Search username"
          v-model="searchInput"
          solo
          @input="searchSuggestions()"
          v-on:focus="menu = true"
          v-on:blur="menu = false"
          v-on="on"
          color="purple"
        >
        </v-text-field>
      </template>
      <v-list v-if="!search.length" height="58px" class="pa-0 ma-0">
        <v-list-item
          v-for="(suggestion, i) in filteredSuggestions"
          :key="'A' + i"
        >
          <v-list-item-icon>
            <h4>{{ suggestion.index + 1 }}</h4>
          </v-list-item-icon>
          <v-list-item-content>
            <v-list-item-title>
              {{ suggestion.username }} | Streak:
              {{ suggestion[account.username + "Streak"] }} | Exp:
              {{ suggestion[account.username + "Exp"] }}
            </v-list-item-title>
          </v-list-item-content>

          <!-- <v-list-item-avatar>
            <v-img :src="item.avatar"></v-img>
          </v-list-item-avatar> -->
        </v-list-item>
        <v-list-item v-if="!filteredSuggestions.length">
          <v-list-item-content>
            <v-list-item-title v-if="searchInput" class="mt-2">
              The username "<strong>{{ searchInput }}</strong
              >" is not found
            </v-list-item-title>
            <v-list-item-title v-if="!searchInput" class="mt-2">
              You have yet to search for a username
            </v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-menu>
  </div>
</template>
<script>
export default {
  name: "RankingsSearchBar",
  props: ["rankings", "account"],
  data() {
    return {
      searchInput: "",
      menu: false,
      search: "",
      filteredSuggestions: [],
    };
  },

  created() {},
  methods: {
    searchSuggestions() {
      this.filteredSuggestions = [];
      if (this.searchInput) {
        this.rankings.forEach((option, index) => {
          let username = option.username;
          let newOption = {
            ...option,
            index,
          };
          if (
            username.toLowerCase().includes(this.searchInput.toLowerCase()) &&
            !this.filteredSuggestions.some(
              (suggestion) => suggestion.username === option.username
            )
          ) {
            this.filteredSuggestions.push(newOption);
          }
        });
      }
    },
  },
};
</script>

<style scoped>
:deep(.searchBarHomeSm.v-text-field.v-text-field--solo:not(.v-text-field--solo-flat)
    > .v-input__control
    > .v-input__slot) {
  padding: 18px;
  border-radius: 15px;
}
:deep(.v-messages.theme--light) {
  display: none !important;
}
:deep(.v-text-field__details) {
  display: none !important;
}

.v-text-field--filled {
  background: white;
  color: white;
}
:deep(.theme--dark.v-card) {
  background: white !important;
  color: F0F0F0;
}
.v-list {
  height: 35vh; /* or any height you want */
  overflow-y: auto;
}
.theme--dark.v-icon {
  color: #6d1bff;
}

:deep(.v-text-field.v-text-field--solo .v-input__control input) {
  color: black !important;
}
:deep(.theme--dark.v-btn.v-btn--disabled:not(.v-btn--flat):not(.v-btn--text):not(.v-btn--outlined)) {
  background-color: #f0f0f0 !important;
  color: black !important;
}
:deep(.theme--dark.v-btn.v-btn--disabled
    .v-icon, .theme--dark.v-btn.v-btn--disabled .v-btn__loading) {
  color: grey !important;
}
.searchBarXs {
  width: 100%;
  margin-top: 8px;
}
.searchBarSm {
  width: 600px;
  margin-top: 8px;
}
.searchBarHomeSm {
  width: 700px;
  margin-top: 8px;
}
</style>
