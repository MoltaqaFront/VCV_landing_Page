<template>
  <div id="contact_us_section" class="footer_content_wrapper">
    <div class="container-xl">
      <div class="row justify-content-between align-items-center">
        <!-- Start:: Logo Wrapper -->
        <div class="col-lg-3 col-xl-2 my-3">
          <div class="logo_wrapper focus_screen">
            <img src="~/assets/media/logo/logo.png" width="120" height="auto" alt="Logo" />
          </div>
        </div>
        <!-- End:: Logo Wrapper -->

        <!-- Start:: Routes Wrapper -->
        <div class="col-lg-3 col-xl-2 d-flex justify-content-center my-3">
          <ul class="footer_routes_list">
            <li class="footer_route">
              <button class="active" @click="scrollToSection('hero_section')"> {{ $t("nav.home") }} </button>
            </li>

            <li class="footer_route">
              <button @click="scrollToSection('about_section')"> {{ $t("nav.about") }} </button>
            </li>

            <li class="footer_route">
              <button @click="scrollToSection('app_screens_section')"> {{ $t("nav.screen") }} </button>
            </li>

            <li class="footer_route">
              <button @click="scrollToSection('download_app_section')"> {{ $t("nav.download") }} </button>
            </li>
            <li class="footer_route">
              <button @click="scrollToSection('contact_us_section')"> {{ $t("nav.contact") }} </button>
            </li>
          </ul>
        </div>
        <!-- End:: Routes Wrapper -->

        <!-- Start:: Contact Info Wrapper -->
        <div class="col-lg-6 col-xl-5 d-flex justify-content-between flex-column flex-lg-row my-3">
          <ul class="contact_info_list">
            <!-- <li class="contact_info_item">
              <span class="icon">
                <i class="fa-regular fa-envelope"></i>
              </span>

              <a href="mailto:info@lamsamotqana.app"><span class="value"> info@lamsamotqana.app </span></a>
            </li> -->

            <li class="contact_info_item">
              <span class="icon">
                <i class="fa-solid fa-fax"></i>
              </span>

              <a :href="'tel:' + phone1"><span class="value">{{ phone1 }}</span></a>
            </li>

            <li class="contact_info_item">
              <span class="icon">
                <i class="fa-solid fa-location-dot"></i>
              </span>

              <span class="value"> {{ address }}
              </span>
            </li>
          </ul>

          <!-- <ul class="social_links_list">
            <li class="social_links_item">
              <a href="https://twitter.com/CaaptainOne" target="_blank" class="icon">
                <i class="fa-brands fa-twitter"></i>
              </a>
            </li>

            <li class="social_links_item">
              <a href="https://www.facebook.com/Captain-one-%D9%83%D8%A7%D8%A8%D8%AA%D9%86-%D9%88%D8%A7%D9%86-100203022791919/" target="_blank" class="icon">
                <i class="fa-brands fa-square-facebook"></i>
              </a>
            </li>

            <li class="social_links_item">
              <a href="https://www.instagram.com/caaptainone/" target="_blank" class="icon">
                <i class="fa-brands fa-instagram"></i>
              </a>
            </li>
          </ul> -->
        </div>
        <!-- End:: Contact Info Wrapper -->
      </div>
    </div>

    <div class="copyrights_contet">
      <h6> {{ $t('copyWrite') }} </h6>
    </div>
  </div>
</template>

<script>
export default {
  name: "TheFooter",

  data() {
    return {
      isLoading: true,

      address: '',
      phone1: '',
    };
  },


  async fetch() {
    try {
      return await this.$axios.get(`setting`).then(response => {
        this.address = response.data.data.address;
        this.phone1 = response.data.data.phone1;
        console.log(response.data.data.title)
      }).catch(error => {
        console.log(error)
      })
    } catch (error) {
      console.log("catch : " + error)
    }
  },

  methods: {
    // START:: SCROLL TO SECTION
    scrollToSection(section_id) {
      if (this.$route.path.includes("/register")) {
        this.$router.push("/");
      } else {
        const selected_section = document.querySelector(`#${section_id}`);
        selected_section.scrollIntoView();
      }
    },
    // END:: SCROLL TO SECTION


  },
}
</script>
