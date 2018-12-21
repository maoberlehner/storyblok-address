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
    </div>

    <div class="Address__field">
      <span class="form__topic">
        Phone
      </span>
      <input
        v-model="model.phone"
        class="uk-form-small uk-width-1-1"
      >
    </div>

    <div class="Address__field">
      <span class="form__topic">
        Fax
      </span>
      <input
        v-model="model.fax"
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
export default {
  mixins: [window.Storyblok.plugin],
  watch: {
    model: {
      deep: true,
      handler(value) {
        this.$emit(`changed-model`, value);
      },
    },
  },
  methods: {
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
</style>
