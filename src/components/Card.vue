<script setup>
import { onMounted } from "vue";
import { productInfos } from "../data/data";
import { gsap } from "gsap";

const fadeAnimation = () => {
  const title = document.querySelector(".title");
  const subtitle = document.querySelector(".subtitle");
  const content = document.querySelector(".content");

  const elements = [title, subtitle, content];

  gsap.fromTo(
    elements,
    {
      y: "50%",
      rotate: 2,
      opacity: 0,
      ease: "power4.out",

      stagger: {
        amount: 0.233,
      },
    },
    {
      y: "0%",
      rotate: 0,
      opacity: 1,
      delay: 0.5,
      duration: 1,
    }
  );
};

const scaleAnimation = () => {
  const img = document.querySelector(".image-container img");

  gsap.fromTo(
    img,
    {
      scale: 1.2,
      ease: "power4.out",
    },
    {
      scale: 1,
      delay: 0.5,
      duration: 1.5,
    }
  );
};

onMounted(() => {
  fadeAnimation();
  scaleAnimation();
});
</script>

<template>
  <section class="card">
    <div class="image-wrapper">
      <div class="image-container">
        <picture>
          <source
            media="(max-width: 1439px)"
            :srcset="`${productInfos.mobileImage}`"
          />
          <source
            media="(min-width: 1440px)"
            :srcset="`${productInfos.desktopImage}`"
          />
          <img :src="productInfos.mobileImage" :alt="productInfos.infoImage" />
        </picture>
      </div>
    </div>
    <div class="content-wrapper">
      <div class="description">
        <h2 class="subtitle">
          {{ productInfos.subtitle }}
        </h2>
        <h1 class="title">
          {{ productInfos.title }}
        </h1>
        <p class="content">
          {{ productInfos.content }}
        </p>
      </div>

      <div class="price">
        <span class="new-price">${{ productInfos.price - 20 }}</span>
        <span class="old-price">${{ productInfos.price }}</span>
      </div>

      <div>
        <button class="btn-primary">
          <div id="circle"></div>
          <a class="content">
            <span><img src="../assets/icon-cart.svg" alt="Icon bag" /></span>Add
            to Cart
          </a>
        </button>
      </div>
    </div>
  </section>
</template>

<style lang="scss">
@import "../styles/main.scss";

.card {
  width: 345px;
  display: flex;
  flex-direction: column;
  overflow: hidden;
  border-radius: 20px;
  background-color: $color-white;

  .image-wrapper {
    height: 25vh;
    overflow: hidden;

    .image-container {
      height: 100%;

      img {
        width: 100%;
        height: 100%;
        object-fit: cover;
      }
    }
  }

  .content-wrapper {
    padding: 25px;

    .subtitle {
      margin-top: 0;
    }

    .price {
      display: flex;
      align-items: center;
      gap: 20px;

      .new-price {
        font-family: "Fraunces", serif;
        color: $color-tiertary;
        font-weight: 700;
        font-size: 2.2rem;
        line-height: 1;
        margin: 15px 0;
      }
      .old-price {
        text-decoration: line-through;
      }
    }

    button {
      width: 100%;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 10px;
      margin-bottom: 0;
    }
  }
}

@media screen and (min-width: 1440px) {
  .card {
    flex-direction: row;
    width: 720px;
    height: 500px;

    .image-wrapper,
    .content-wrapper {
      width: 50%;
    }
    .image-wrapper {
      height: 100%;
    }
    .content-wrapper {
      padding: 35px;
    }
  }
}
</style>
