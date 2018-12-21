<template>
  <div class="Address">
    <div class="Address__field">
      <span class="form__topic">
        Street
      </span>
      <input
        v-model="model.street"
        class="uk-form-small uk-width-1-1"
      >
    </div>

    <div class="Address__field">
      <span class="form__topic">
        Town
      </span>
      <input
        v-model="model.town"
        class="uk-form-small uk-width-1-1"
      >
    </div>

    <div class="Address__field">
      <span class="form__topic">
        Postal code
      </span>
      <input
        v-model="model.postal_code"
        class="uk-form-small uk-width-1-1"
      >
    </div>

    <div class="Address__field">
      <span class="form__topic">
        Country
      </span>
      <input
        v-model="model.country"
        class="uk-form-small uk-width-1-1"
      >
    </div>

    <div class="Address__field">
      <span class="form__topic">
        Coordinates
      </span>
      <div class="uk-grid">
        <label class="uk-width-1-2">
          Latitude
          <input
            v-model.number="model.latitude"
            class="uk-form-small uk-width-1-1"
          >
        </label>
        <label class="uk-width-1-2">
          Longitude
          <input
            v-model.number="model.longitude"
            class="uk-form-small uk-width-1-1"
          >
        </label>
      </div>
      <a
        class="blok__full-btn uk-margin-small-top"
        @click="coordinatesByAddress"
      >
        <i class="uk-icon-search uk-margin-small-right"/>
        Generate from address
      </a>
      <p
        v-if="latLngNotFound"
        class="Address__error"
      >
        Could not find coordinates for the given address.
      </p>
    </div>

    <div class="Address__field">
      <span class="form__topic">
        Phone
      </span>
      <input
        ref="phone"
        v-model.lazy="model.phone"
        class="uk-form-small uk-width-1-1"
      >
    </div>

    <div class="Address__field">
      <span class="form__topic">
        Fax
      </span>
      <input
        ref="fax"
        v-model.lazy="model.fax"
        class="uk-form-small uk-width-1-1"
      >
    </div>

    <div class="Address__field">
      <span class="form__topic">
        E-Mail
      </span>
      <input
        v-model="model.email"
        type="email"
        class="uk-form-small uk-width-1-1"
      >
    </div>
  </div>
</template>

<script>
import Cleave from 'cleave.js';
import 'cleave.js/dist/addons/cleave-phone.at';

// The URL of the OpenStreetMap endpoint
// for fetching location data by address.
const ENDPOINT = `https://nominatim.openstreetmap.org/search`;

export default {
  mixins: [window.Storyblok.plugin],
  data() {
    return {
      latLngNotFound: false,
    };
  },
  watch: {
    model: {
      deep: true,
      handler(value) {
        this.$emit(`changed-model`, value);
      },
    },
  },
  mounted() {
    const phoneOptions = {
      phone: true,
      phoneRegionCode: `AT`,
    };
    // eslint-disable-next-line no-new
    new Cleave(this.$refs.phone, phoneOptions);
    // eslint-disable-next-line no-new
    new Cleave(this.$refs.fax, phoneOptions);
  },
  methods: {
    async coordinatesByAddress() {
      try {
        // Reset the error message before
        // fetching new location data.
        this.latLngNotFound = false;

        // Here we build the query string with
        // all the address data available to us
        const queryString = [
          `city=${encodeURI(this.model.town)}`,
          `country=${encodeURI(this.model.country)}`,
          `postalcode=${encodeURI(this.model.postal_code)}`,
          `street=${encodeURI(this.model.street)}`,
          `format=jsonv2`,
        ].join(`&`);

        // We use the new `fetch` API to query
        // the public OpenStreetMap API.
        const rawResponse = await fetch(`${ENDPOINT}?${queryString}`);
        const responseJson = await rawResponse.json();
        const bestMatch = responseJson[0];

        // Throw error if address is not found.
        if (!bestMatch) throw new Error(`Address not found`);

        // If OpenStreetMap was able to find us
        // some coordinates, we update our model.
        this.model.latitude = parseFloat(bestMatch.lat);
        this.model.longitude = parseFloat(bestMatch.lon);
      } catch (error) {
        this.latLngNotFound = true;
      }
    },
    initWith() {
      return {
        country: ``,
        email: ``,
        fax: ``,
        latitude: null,
        longitude: null,
        phone: ``,
        postal_code: ``,
        street: ``,
        town: ``,
        plugin: `address`,
      };
    },
  },
};
</script>

<style>
.Address__field + .Address__field {
  margin-top: 10px;
}

.Address__error {
  margin-top: 5px;
  margin-bottom: 0;
  color: #d85030;
}
</style>
