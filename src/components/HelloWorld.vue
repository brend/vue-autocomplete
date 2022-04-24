<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12">
        <th-autocomplete
          v-model:search="search"
          v-model:selection="selection"
          :items="cities"
          :isLoading="isLoading"
        ></th-autocomplete>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <p>Searching for: "{{search}}"</p>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <p>Selected: "{{selection}}"</p>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import ThAutocomplete from './ThAutocomplete.vue';
import {debounce} from 'lodash';

export default {
  components: { ThAutocomplete },
  name: 'HelloWorld',

  data: () => ({
    cities: [],
    search: '',
    selection: '',
    isLoading: false,
  }),

  watch: {
    search(...args) {
      this.debouncedWatch(...args);
    },
  },
  created() {
    this.debouncedWatch = debounce((val, oldValue) => {
      console.log("loading suggestions for", val, oldValue);
      this.isLoading = true;
      this.cities = [val + "heim", val + "burg", val + "dorf"];
      this.isLoading = false;
    }, 500);
  },
  beforeUnmount() {
    this.debouncedWatch.cancel();
  },
}
</script>
