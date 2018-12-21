<template>
  <div class="Address"/>
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
