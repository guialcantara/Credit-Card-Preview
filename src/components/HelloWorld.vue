<template>
  <div id="card-page">
    <nav>
      <h2>Guilherme Alcantara</h2>
    </nav>
    <main>
      <aside>
        <ColorPicker
          style="width: 218px"
          theme="dark"
          :color="color01"
          :sucker-hide="true"
          @changeColor="changeColor"
        />
        <ColorPicker
          style="width: 218px"
          theme="dark"
          :color="color02"
          :sucker-hide="true"
          @changeColor="changeColor02"
        />
        <input v-model="name" type="text" name="" />
      </aside>
      <section>
        <div class="card-container">
          <div class="card">
            <div class="card-front" :style="cardColor">
              <img class="positioning" src="../assets/logo.png" alt="" />
              <p class="positioning">{{ name }}</p>
            </div>
            <div class="card-back" :style="cardColorBack">
              <p class="positioning">aaaaaaaaaaaaaaaaa</p>
            </div>
          </div>
        </div>
      </section>
    </main>
  </div>
</template>

<script>
import { ColorPicker } from "vue-color-kit";
import "vue-color-kit/dist/vue-color-kit.css";
export default {
  components: {
    ColorPicker,
  },
  data() {
    return {
      name: "",
      color01: "#000000",
      color02: "#414141",
    };
  },
  computed: {
    cardColor() {
      return {
        backgroundImage: `linear-gradient(315deg, ${this.color01} 0%, ${this.color02} 74%)`,
      };
    },
    cardColorBack() {
      return {
        backgroundImage: `linear-gradient(52deg, ${this.color01} 0%, ${this.color02} 74%)`,
      };
    },
  },
  methods: {
    changeColor(color01) {
      const { r, g, b, a } = color01.rgba;
      this.color01 = `rgba(${r}, ${g}, ${b}, ${a})`;
    },
    changeColor02(color02) {
      const { r, g, b, a } = color02.rgba;
      this.color02 = `rgba(${r}, ${g}, ${b}, ${a})`;
    },
  },
};
</script>

<style scoped lang="scss">
#card-page {
  display: flex;
  flex-direction: column;
  height: 100vh;
  overflow: hidden;
  background-image: url("../assets/bg.png");
  background-size: cover;
  background-repeat: no-repeat;

  nav {
    width: 100%;
    height: 80px;
    text-align: center;
    color: white;
    padding: 10px 32px;
  }
  main {
    display: flex;
    height: 100%;

    aside {
      display: flex;
      flex: 1;
      padding: 0 32px;
      align-items: center;
      justify-content: center;
    }

    section {
      display: flex;
      flex: 1;
      padding: 0 32px;
      align-items: center;
      justify-content: center;

      .card-container {
        position: relative;
        background-color: transparent;
        width: 400px;
        height: 300px;
        perspective: 1000px;
        animation: bounce ease-in-out 2.5s infinite;

        .card {
          position: relative;
          width: 100%;
          height: 100%;
          text-align: center;
          transition: transform ease 1.6s;
          transform-style: preserve-3d;
        }

        &:hover .card {
          transform: rotateY(180deg) rotate(-30deg) skew(25deg, 6deg)
            scale(1.05) skewY(-20deg);
        }

        .card-front {
          transform: rotate(20deg) skew(-15deg, 3deg);

          img {
            position: absolute;
            width: 60px;
            top: 20px;
            left: 320px;
          }

          p {
            min-width: 360px;
            max-width: 3px;
            text-align: left;
            position: absolute;
            color: white;
            top: 80%;
            left: 25px;
            font-weight: bold;
          }
        }

        .card-back {
          transform: rotateY(180deg) rotate(-25deg) skew(15deg, 0deg);
        }

        .card-front,
        .card-back {
          width: 400px;
          height: 240px;
          border-radius: 15px;
          position: absolute;
          -webkit-backface-visibility: hidden;
          backface-visibility: hidden;
          box-shadow: 13px 13px 13px 0px rgba(0, 0, 0, 0.75);
        }
      }
    }
  }
}
@keyframes bounce {
  0% {
    transform: translateY(0%);
  }
  50% {
    transform: translateY(5%);
  }
  100% {
    transform: translateY(0%);
  }
}
</style>
