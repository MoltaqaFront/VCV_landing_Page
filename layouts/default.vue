<template>
  <v-app :class="[{ rtl: $i18n.locale == 'ar' }, { ltr: $i18n.locale == 'en' }]">
    <div class="user_layout">
      <!-- Start:: Layout Navbar -->
      <TheNavbar />
      <!-- End:: Layout Navbar -->

      <Nuxt />

      <!-- Start:: Layout Footer -->
      <TheFooter />
      <!-- End:: Layout Footer -->
    </div>
  </v-app>
</template>

<script>
import TheNavbar from "~/components/structure/TheNavbar";
import TheFooter from "~/components/structure/TheFooter";

export default {
  name: 'DefaultLayout',

  head() {
    return {
      titleTemplate: "vcv App - %s",
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: this.$t("meta.desc"),
        }
      ],
    }
  },

  components: {
    TheNavbar,
    TheFooter,
  },
}
</script>

<style lang="scss" scoped>
.user_layout .header_content_wrapper {
  background-color: var(--main_theme_clr);
}
</style>
