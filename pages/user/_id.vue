<template>
  <client-only>
    <div class="user_profile">
      <div class="container">
        <div class="row align-items-center justify-content-center">

          <div class="col-lg-10 col-12">

            <div class="all_content">

              <div class="info_profile">
                <div class="image" v-if="user_image">
                  <img :src="user_image" alt="user image">
                </div>
                <h2>{{ user_name }}</h2>
                <p class="address">
                  <span v-if="user_city !== ''">{{ user_city }} -</span>
                  <span v-if="user_country !== ''">{{ user_country }} -</span>
                  <span v-if="user_job !== ''">{{ user_job }}</span>
                </p>
              </div>

              <div class="description">
                <p>{{ user_bio }}</p>
              </div>

              <!-- v-for="(item, index) in items" :key="'g' + index" -->
              <ul class="list_advantage">
                <li>
                  <span class="title">{{ $t('user.career') }}</span>
                  <span>{{ user_career }}</span>
                </li>
                <li>
                  <span class="title">{{ $t('user.level') }}</span>
                  <span>{{ user_level }}</span>
                </li>
                <li>
                  <span class="title">{{ $t('user.experience') }}</span>
                  <span>{{ user_experience }}</span>
                </li>
              </ul>

              <div class="video">

                <div class="upload_yet" v-if="user_video == null">
                  <p>{{ $t('user.upload_yet') }}</p>
                </div>

                <video controls v-else>
                  <source :src="'https://jobsvcv.com/' + user_video" type="video/mp4">
                  <source :src="user_video" type="video/ogg">
                </video>


              </div>

              <a :href="'https://jobsvcv.com/' + user_cv" class="download_cv" target="_self" download
                v-if="user_cv !== ''">
                {{ $t('user.download_cv') }}
              </a>

              <div class="skills" v-if="user_skills.length">
                <h3>{{ $t('user.skills') }}</h3>

                <ul>
                  <li v-for="(item, index) in user_skills" :key="'g' + index">
                    <span class="talent">{{ item }}</span>
                  </li>
                </ul>
              </div>


              <div class="istp" v-if="user_label_type">

                <button class="all_link" @click="show_info = !show_info">
                  <span class="title">{{ user_label }}</span>
                  <span class="content">
                    <span>{{ user_label_type }}</span>
                    <i class="fa-solid fa-chevron-down"></i>
                  </span>
                </button>

                <transition name="fade">
                  <div v-if="show_info" class="show_info_div">
                    <div class="info_profile last_info">
                      <div class="image" v-if="user_label_image">
                        <img :src="user_label_image" alt="user image">
                      </div>
                      <p class="address">{{ $t('user.user_label_image') }} </p>
                      <h2> {{ user_label }} ({{ user_label_type }})</h2>

                      <p style="padding-top:15px">{{ label_excerpt }}</p>
                      <span v-html="label_content"></span>
                    </div>
                  </div>
                </transition>
              </div>

            </div>

          </div>

        </div>
      </div>
    </div>
  </client-only>
</template>

<script>


export default {

  head() {
    return {
      title: "user profile",
    }
  },

  layout: 'default',


  data() {
    return {
      show_info: true,

      user_name: '',
      user_image: '',
      user_city: '',
      user_country: '',
      user_job: '',
      user_bio: '',
      user_career: '',
      user_level: '',
      user_video: null,
      user_cv: '',
      user_label: '',
      user_label_image: '',
      user_label_type: '',
      user_skills: [],
      user_experience: '',
      label_content: '',
      label_excerpt: ''
    }
  },

  async fetch() {
    try {
      return await this.$axios.post(`gust/users/${this.$route.params.id}`).then(response => {

        this.loading = true;

        console.log(response.data)

        this.user_name = response.data.data.name;
        this.user_image = response.data.data.image;
        this.user_city = response.data.data.city;
        this.user_country = response.data.data.country;
        this.user_job = response.data.data.job;
        this.user_bio = response.data.data.bio;
        this.user_career = response.data.data.career;
        this.user_level = response.data.data.level;
        this.user_experience = response.data.data.experience;
        this.user_video = response.data.data.video.url;
        this.user_cv = response.data.data.cv;
        this.user_skills = response.data.data.skills;
        this.user_label = response.data.data.label;
        this.user_label_image = response.data.data.label_image;
        this.user_label_type = response.data.data.label_type;

        this.label_content = response.data.data.label_object.content;
        this.label_excerpt = response.data.data.label_object.excerpt;

        // console.log(response.data.data)

      }).catch(error => {
        console.log(error)
      })
    } catch (error) {
      console.log("catch : " + error)
    }
  },

  created() {

  },


  computed: {
  },

  //  when component load

  mounted() {

    window.scrollTo(0, 0);
    this.$nextTick(() => {
      window.scrollTo(0, 0);
    });
  },


  // All methods and logic

  methods: {

  }
}
</script>

<style lang="scss" scoped>
.validation_message {
  font-size: 13px;
  color: red;
}

.user_profile {
  margin: 150px 0 50px;

  .all_content {
    text-align: center;
    padding: 40px 60px;
    background: #fff;
    box-shadow: 0px 13px 66px #86848429;

    .info_profile {

      &.last_info {

        h2 {
          color: var(--main_theme_clr);
          margin-top: 3px;
        }

        .address {
          padding-top: 10px;
          color: #000
        }

      }

      .image {
        width: 100px;
        height: 100px;
        margin: auto;

        img {
          width: 100%;
          height: 100%;
          border-radius: 50%
        }
      }

      h2 {
        font-size: 22px;
        font-weight: 800;
        margin: 20px 0 0;
      }

      .address {
        font-size: 18px;
        color: #aaa7a7;
      }
    }

    .list_advantage {
      display: flex;
      flex-direction: column;
      gap: 10px;
      margin: 30px 0;

      li {

        display: flex;
        justify-content: center;
        align-items: center;
        gap: 20px;

        span {
          color: #000;
          font-size: 18px;


          &.title {
            color: var(--main_theme_clr);
            font-size: 20px;
            font-family: "Poppins Light" !important;
          }

        }
      }
    }

    .video {
      margin: 30px 0;

      video {
        width: 100%;
        height: 300px
      }

      .upload_yet {
        p {
          color: #000;
          font-size: 20px;
          font-weight: bold;
          background-color: #DDD;
          padding: 20px 30px;
        }
      }
    }

    a.download_cv {
      height: 47px;
      width: 150px;
      transition: 0.7s;
      text-transform: capitalize;
      border: 1px solid transparent;
      outline: 0;
      cursor: pointer;
      font-size: 16px;
      box-shadow: 0 0 20px rgba(1, 63, 205, 0.3411764706);
      border-radius: 50px;
      text-align: center;
      color: #fff;
      background: #0081a8;
      margin: auto;
      display: flex;
      justify-content: center;
      align-items: center;
    }

    .skills {
      h3 {
        font-size: 22px;
        font-weight: 800;
        margin: 20px 0 0;
      }

      ul {
        display: flex;
        gap: 20px;
        flex-wrap: wrap;
        margin-top: 30px !important;


        li {
          span.talent {
            background-color: #DDD;
            color: var(--main_theme_clr);
            min-width: 80px;
            height: 40px;
            display: flex;
            justify-content: center;
            align-items: center;
            font-weight: bold;
            border-radius: 50px;
            width: auto;
            padding: 20px;
          }
        }
      }
    }

    .istp {

      .all_link {
        display: flex;
        align-items: center;
        margin: 30px 0;
        justify-content: space-between;
        width: 100%;
        background: #EEE;
        padding: 8px 20px;
      }

      .content {
        color: var(--main_theme_clr);
        font-size: 20px;
        font-weight: bold;
      }
    }
  }
}


@media(max-width:991px) {
  .user_profile .all_content {
    padding: 30px 15px;
  }
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease-in-out;
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>
