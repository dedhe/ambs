<template>
  <div style="background:#f5f5f5">
    <header class="header">
      <div class="logo">
        <img src="../assets/logo.png" alt="logo ambassador" />
        <div class="navigator">
          <v-btn outline color="red darken-4" small v-scroll-to="'#about'">About Us</v-btn>
          <v-btn outline color="red darken-4" small v-scroll-to="'#portofolio'">portofolio</v-btn>
          <v-btn outline color="red darken-4" small v-scroll-to="'#galeri'">Terbaru</v-btn>
          <v-btn outline color="red darken-4" small v-scroll-to="'#contact'">contact us</v-btn>
        </div>
      </div>
      <div class="cover">
        <video src="../assets/video.mp4" autoplay loop muted class="myvideo"></video>
      </div>
    </header>

    <section style="background:#fff;" id="about">
      <v-container>
        <v-layout row wrap>
          <v-flex xs12 sm4 class="hh">
            <div class>
              <h2 class="heading">Visi Kami</h2>
              <p
                style="text-align:left"
              >Menjadi pengembang property yang mengutamakan inovasi dan pelayanan yang terbaik untuk meningkatkan kualitas kehidupan manusia</p>
            </div>
          </v-flex>
          <v-flex xs12 sm4 class="hh">
            <div class>
              <h2 class="heading">Misi</h2>
              <p
                style="text-align:left"
              >1. Menjadi perusahaan yang selalu mengedepankan kualitas dalam mengembangkan sebuah komplek hunian.</p>
              <p>2. Selalu berinovasi dan memberikan nilai tambah untuk memberikan keuntungan jangka panjang bagi partner bisnis, investor, karyawan dan masyarakat.</p>
              <p>3. Menjadi perusahaan yang mengambil bagian dalam mendukung program pemerintah untuk pengembangan kota dan sumber daya manusia.</p>
              <p>4. Menjaga tata kelola yang sehat dalam perusahaan untuk menjaga kepercayaan bagi para partner bisnis, investor, karyawan dan masyarakat.</p>
            </div>
          </v-flex>
          <v-flex xs12 sm4 class="hh">
            <div class>
              <h2 class="heading">Nilai</h2>
              <p>
                <b>1. Kenyamanan.</b>
                <br />Kami memiliki komitmen untuk menyediakan hunian yang nyaman bagi para penghuninya. Akses ke sarana umum mudah dijangkau adalah bagian dari standard kami dalam menentukan lokasi project.
              </p>
              <p>
                <b>
                  2. Keamanan.
                  <br />
                </b>
                Apalah arti sebuah kenyamanan tanpa keamanan yang terjamin, bukan hanya keamanan di dalam perumahan, namun keamanan dari sisi legalitas lahan juga menjadi faktor utama di setiap project kami.
              </p>
              <p>
                <b>3. Kebanggaan.</b>
                <br />Design rumah yang dibangun dibuat minimalis modern, elegan dan mempunyai keunikan dari design bangunan dikelasnya. Dan selalu mengikuti perkembangan design, sehingga tak lekang oleh waktu.
              </p>

              <p>
                <b>4. Kenaikan nilai.</b>
                <br />Kami selalu memilih lokasi yang sedang berkembang untuk setiap project nya, sehingga menjadikan nilai investasinya selalu naik.
              </p>
            </div>
          </v-flex>
        </v-layout>
      </v-container>
    </section>
    <section id="portofolio">
      <v-container>
        <v-layout row wrap>
          <v-flex xs12 sm12>
            <div class="isi" style="text-align:center">
              <h2 class="heading">Our Portofolio</h2>
            </div>
          </v-flex>

          <v-flex xs6 sm3 class="hh" v-for="(dt, key) in portos" :key="key">
            <div class="porto" @click="detailPorto(dt)">
              <img :src="getUrl+dt.foto" alt="portofolio 1" class />
            </div>
          </v-flex>
        </v-layout>
      </v-container>
    </section>
    <section style="background:white; padding: 20px 0px 20px 0px;" id="galeri">
      <div class="cover">
        <video src="../assets/amb5.mp4" autoplay loop muted class="myvideo"></video>
      </div>
    </section>
    <section id="contact">
      <iframe
        src="https://maps.google.com/maps?q=ambassadorland%20singkawang&t=&z=13&ie=UTF8&iwloc=&output=embed"
        frameborder="0"
        scrolling="no"
        marginheight="0"
        marginwidth="0"
      ></iframe>
    </section>
    <section style="background:brown">
      <v-container style="background:brown">
        <v-layout row wrap>
          <v-flex x12 class="text-xs-center">
            <h3 style="color: white">© ambassadorland.co.id 2017-{{new Date().getFullYear()}}</h3>
          </v-flex>
        </v-layout>
      </v-container>
    </section>

    <v-dialog v-model="dialog" persistent max-width="600px">
      <v-card v-if="detail">
        <v-card-title style="justify-content: center">
          <h1 class="headline">{{detail.judul}}</h1>
        </v-card-title>
        <v-card-text>
          <v-container grid-list-md>
            <v-layout wrap>
              <v-flex xs12>
                <p>
                 {{detail.isi}} </p>
              </v-flex>
            </v-layout>
          </v-container>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="blue darken-1" flat @click="dialog = !dialog">Close</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
import axios from "~/plugins/axios";
export default {
  data() {
    return {
      dialog: false,
      getUrl: "http://localhost:2000/static/",
      portos: [],
      detail : null
    };
  },
  created() {
    this.initialize();
  },

  methods: {
    initialize() {
      axios
        .get("/porto")
        .then(res => {
          this.portos = res.data;
        })
        .catch(err => console.log(err));
    },
    detailPorto(dt) {
      console.log(dt);
      this.detail = dt
      this.dialog = true
    }
  }
};
</script>

<style lang="scss">
iframe {
  height: 500px;
  width: 100%;
}
#portofolio {
  padding: 20px 0px 20px 0px;
  background: brown;
  h2 {
    color: white;
  }
}
h2 {
  font-size: 30px;
  margin-bottom: 15px;
  // border-bottom: #b302028c 1px solid;
  padding-bottom: 10px;
  border-width: thick;
  // font-family: fantasy;
  color: rgb(173, 0, 0);
}
.container {
  max-width: 1050px;
}
.header {
  background: white;
  padding-top: 20px;
  position: relative;
  z-index: 4;
  width: 100%;
  text-align: center;

  .logo {
    position: relative;
    width: 100%;
    height: auto;
    .navigator {
      position: relative;
      background: white;
      border-radius: 20px;
      width: 70%;
      margin: auto;
      box-shadow: 0px 7px 0px 8px rgb(179, 2, 2);
    }
    img {
      width: 220px;
      height: 100px;
    }
  }
  .cover {
    z-index: 2;
    // background-image: url("../assets/cover.jpg");
    background-attachment: fixed;
    background-size: 100% 100%;
    // border-radius: 59px 180px 59px 180px;
    // background-position: 1px;

    height: 500px;
    width: 100%;
  }
}
.cover {
  z-index: 2;
  // background-image: url("../assets/cover.jpg");
  background-attachment: fixed;
  background-size: 100% 100%;
  // border-radius: 59px 180px 59px 180px;
  // background-position: 1px;

  height: 500px;
  width: 100%;
}
.hh {
  z-index: 1;
  padding: 10px;

  .isi {
    text-align: justify;
    width: 100%;
    box-shadow: rgba(0, 0, 0, 0.12) 0px 0px 7px;
    border-radius: 5px;
    padding: 30px;
    background: white;
    &:hover {
      box-shadow: rgba(214, 25, 25, 0.521) 0px 0px 7px;
    }
  }
}

.bulat-merah {
  background-color: red;
  width: 100%;
  height: 500px;
  top: 0;
  z-index: 0;
  position: absolute;
}
.porto {
  img {
    background: white;
    width: 100%;
    border: 1px solid #ddd; /* Gray border */
    border-radius: 4px; /* Rounded border */
    padding: 5px;
    &:hover {
      box-shadow: rgba(214, 25, 25, 0.521) 0px 0px 7px;
      background: linear-gradient(90deg, #369898, #5eeebb);
      cursor: pointer;
      transform: translateY(-19px);
      transition: all 0.3s;
    }
  }
}
.myvideo {
  position: static;
  z-index: 0;
  // background: url(mel.jpg) no-repeat;
  background-size: 100% 100%;
  top: 0px;
  left: 0px; /* fixed to left. Replace it by right if you want.*/
  min-width: 100%;
  min-height: 100%;
  width: auto;
  //height: auto;
  height: 300px;
}

@media (min-width: 320px) and (max-width: 600px) {
  .myvideo {
    position: static;
    z-index: 0;
    min-width: 100%;
    min-height: 100%;
    width: 150px;
    //height: auto;
    height: 150px;
  }
  .cover {
    height: 200px;
  }
  //CSS
  .header {
    background: white;
    padding-top: 20px;
    position: relative;
    z-index: 4;
    width: 100%;
    text-align: center;

    .cover {
      z-index: 2;
      //background-image: url("../assets/cover.jpg");
      background-attachment: fixed;
      background-size: 100% 100%;
      // border-radius: 59px 180px 59px 180px;
      // background-position: 1px;

      height: 280px;
      width: 100%;
      .navigator {
        background: white;
        border-radius: 20px;
        width: 70%;
        margin: auto;
        box-shadow: 0px 7px 0px 8px rgb(179, 2, 2);
      }
    }
  }
}
</style>
