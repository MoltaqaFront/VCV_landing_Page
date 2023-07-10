<template>
  <div id="about_section" class="about_section_content_wrapper">
    <div class="row align-items-center px-5">
      <!-- Start:: Section Image -->
      <div class="col-md-6" data-aos-once="false" :data-aos="$i18n.locale == 'ar' ? 'fade-left' : 'fade-right'"
        data-aos-delay="500" data-aos-duration="1000">
        <div class="section_image_wrapper">
          <img src="~/assets/media/images/mobileScreens/two_mobile.png" width="450" height="350"
            alt="About Us Section Image" loading="lazy" />
        </div>
      </div>
      <!-- End:: Section Image -->

      <!-- Start:: Section Text -->
      <div class="col-md-6">
        <!-- <div class="logo_wrapper">
          <img src="~/assets/media/logo/logo.png" alt="Logo" width="180" height="180" data-aos-once="false"
            data-aos="fade" data-aos-delay="500" data-aos-duration="1000" loading="lazy" />
        </div> -->

        <h4 class="section_subtitle" data-aos-once="false" data-aos="fade" data-aos-delay="600" data-aos-duration="1000">
          {{ about_title }}
        </h4>
        <h2 class="section_title" data-aos-once="false" data-aos="fade" data-aos-delay="700" data-aos-duration="1000">
          {{ about_excerpt }}
        </h2>

        <div class="section_desc" data-aos-once="false" data-aos="fade" data-aos-delay="800" data-aos-duration="1000"
          v-html="about_content"></div>
      </div>
      <!-- End:: Section Text -->
    </div>
  </div>
</template>

<script>
export default {
  name: "AboutSection",

  async fetch() {
    try {
      return await this.$axios.get(`pages/2`).then(response => {
        this.about_title = response.data.data.title;
        this.about_excerpt = response.data.data.excerpt;
        this.about_content = response.data.data.content;
        console.log(response.data.data.title)
      }).catch(error => {
        console.log(error)
      })
    } catch (error) {
      console.log("catch : " + error)
    }
  },
 
  data() {
    return {
      isLoading: true,

      about_title: '',
      about_excerpt: '',
      about_content: ''
    };
  },
};
</script>

<style lang="scss" scoped>
.about_section_content_wrapper {
  padding-block: 50px;
  overflow-x: hidden;

  .section_image_wrapper {
    display: flex;
    align-items: center;
    justify-content: center;

    img {
      width: 50%;
      height: auto;
    }
  }

  .section_subtitle {
    margin-block: 20px 0;
    color: var(--main_theme_clr);
    font-size: 30px;
  }

  .section_title {
    margin-block: 25px;
    color: var(--main_theme_clr);
    font-weight: 800;
    font-size: 40px;
    width: 70%;
  }

  .section_desc {
    word-break: break-word;
    word-spacing: 2px;
    font-size: 16px;
    color: var(--light_gray_clr);
    line-height: 1.6;
    text-align: start;
    width: 85%;
  }
}

@media (max-width: 850px) {
  .about_section_content_wrapper {
    padding-block: 30px;

    .section_image_wrapper {
      img {
        width: 90%;
      }
    }

    .logo_wrapper {
      display: flex;
      justify-content: center;
    }

    .section_subtitle {
      margin-block: 20px 0;
      font-size: 22px;
      text-align: center;
    }

    .section_title {
      margin-block: 25px;
      font-size: 25px;
      width: 100%;
      text-align: center;
    }

    .section_desc {
      word-break: break-word;
      word-spacing: 2px;
      font-size: 16px;
      text-align: center;
      width: 100%;
    }
  }
}
</style>
