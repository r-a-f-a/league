<template>
  <div class="wrapper">
    <div class="clash-card barbarian">
      <div class="clash-card__image clash-card__image--barbarian">
        <img
          :src="`http://ddragon.leagueoflegends.com/cdn/img/champion/splash/${name}_0.jpg`"
          alt="SplashArt"
        />
      </div>
      <div class="clash-card__level clash-card__level--barbarian">
        {{ details.title }}
      </div>
      <div class="clash-card__unit-name">{{ name }}</div>
      <div class="clash-card__unit-description">{{ details.lore }}</div>

      <div
        class="clash-card__unit-skills clash-card__unit-stats--barbarian clearfix"
      >
        <div class="one-third">
          <div class="stat">Q</div>
            <img class="img-icon"
              
              :src="`http://ddragon.leagueoflegends.com/cdn/11.10.1/img/spell/${name}Q.png`"
            />
        </div>

        <div class="one-third">
          <div class="stat">W</div>
            <img class="img-icon"
              :src="`http://ddragon.leagueoflegends.com/cdn/11.10.1/img/spell/${name}W.png`"
            />
        </div>

        <div class="one-third ">
          <div class="stat">E</div>
            <img class="img-icon"
              :src="`http://ddragon.leagueoflegends.com/cdn/11.10.1/img/spell/${name}E.png`"
            />
        </div>

        <div class="one-third no-border">
          <div class="stat">R</div>
            <img class="img-icon"
              :src="`http://ddragon.leagueoflegends.com/cdn/11.10.1/img/spell/${name}R.png`"
            />
        </div>
        
      </div>
    </div>
    <!-- end card -->
  </div>
  <!-- end wrapper -->
</template>

<script>
import axios from "axios";
export default {
  name: "card-champ",
  props: ["champion"],
  components: {},
  data() {
    return {
      details: {},
    };
  },
  created() {
    this.getInfo();
  },
  mounted() {},
  computed: {
    name() {
      let name = this.champion.toLowerCase();
      return name.charAt(0).toUpperCase() + name.slice(1);
    },
  },
  methods: {
    getInfo() {
      axios
        .get(
          `http://ddragon.leagueoflegends.com/cdn/9.19.1/data/pt_BR/champion/${this.name}.json`
        )
        .then((result) => {
          console.log("RESULT DATA", result);
          this.details = result.data.data[this.name];
        });
    },
  },
};
</script>
<style lang="scss" scoped>
@import url(https://fonts.googleapis.com/css?family=Lato:400,700,900);

$border-radius-size: 14px;
$barbarian: #109c91;

*,
*:before,
*:after {
  box-sizing: border-box;
}

body {
  background: linear-gradient(
      to bottom,
      rgba(140, 122, 122, 1) 0%,
      rgba(175, 135, 124, 1) 65%,
      rgba(175, 135, 124, 1) 100%
    )
    fixed;
  background: url("https://s3-us-west-2.amazonaws.com/s.cdpn.io/195612/coc-background.jpg")
    no-repeat center center fixed;
  background-size: cover;
  font: 14px/20px "Lato", Arial, sans-serif;
  color: #9e9e9e;
  margin-top: 30px;
}

.slide-container {
  margin: auto;
  width: 600px;
  text-align: center;
}

.wrapper {
  padding-top: 40px;
  padding-bottom: 40px;

  &:focus {
    outline: 0;
  }
}

.clash-card {
  background: white;
  width: 300px;
  display: inline-block;
  margin: auto;
  border-radius: $border-radius-size + 5;
  position: relative;
  text-align: center;
  box-shadow: -1px 15px 30px -12px black;
  z-index: 9999;
  padding: 2px;
}

.clash-card__image {
  position: relative;
  height: 230px;
  margin-bottom: 35px;
  border-top-left-radius: $border-radius-size;
  border-top-right-radius: $border-radius-size;
}

.clash-card__image--barbarian {
  background: url("https://s3-us-west-2.amazonaws.com/s.cdpn.io/195612/barbarian-bg.jpg");
  img {
    width: 100%;
    height: 100%;
    position: center;
    border-radius: $border-radius-size + 5;
  }
}

.clash-card__level {
  text-transform: uppercase;
  font-size: 12px;
  font-weight: 700;
  margin-bottom: 3px;
}

.clash-card__level--barbarian {
  color: $barbarian;
}

.clash-card__unit-name {
  font-size: 26px;
  color: black;
  font-weight: 900;
  margin-bottom: 5px;
}

.clash-card__unit-description {
  padding: 20px;
  margin-bottom: 10px;
}

.clash-card__unit-stats--barbarian {
  background: $barbarian;

  .one-third {
    border-right: 1px solid #bd7c2f;
  }
}


.clash-card__unit-skills {
  color: white;
  font-weight: 700;
  border-bottom-left-radius: $border-radius-size;
  border-bottom-right-radius: $border-radius-size;


  .one-third {
    width: relative;
    float: left;
    padding-right:4px;
    padding-bottom: 10px;
    margin-left: 5px;
    
    
  }

  .stat {
    position: center;
    font-size: 20px;
    margin-bottom: 10px;
  }

  .no-border {
    border-right: none;
  }
}

.clearfix:after {
  visibility: hidden;
  display: block;
  font-size: 0;
  content: " ";
  clear: both;
  height: 0;
}

.slick-prev {
  left: 100px;
  z-index: 999;
}

.slick-next {
  right: 100px;
  z-index: 999;
}

.img-icon {
  border-radius:4px;
}

</style>
