<script setup>
import mainPhoto from "../assets/images/hero.svg";
import { themeColor } from "../data/items";

const heroHeading = "UEH University";
const buttonSeeFeature = "See Features";
const buttonPricing = "Others";
</script>

<template>
  <div class="untree_co-hero" id="home-section">
    <div class="container">
      <div class="row align-items-center">
        <div class="col-12">
          <div class="dots"></div>
          <div class="row align-items-center">
            <div
              class="col-lg-7 ml-auto order-lg-2"
              data-aos="fade-right"
              data-aos-delay="400"
            >
              <img :src="mainPhoto" alt="Image" class="img-fluid" />
            </div>
            <div class="col-lg-5">
              <h1 class="heading" data-aos="fade-up" data-aos-delay="0">
                {{ heroHeading }}
              </h1>
              <div class="excerpt" data-aos="fade-up" data-aos-delay="100">
                <p>
                  University of Economics Ho Chi Minh City is one of the country's key universities. After 48 years of establishment and development, with a team of professors and lecturers trained in prestigious domestic and international universities, with in-depth expertise and high scientific reputation. UEH has made many practical contributions to scientific research through many international publications, key research topics at the goverment and local levels, and applied research projects, with an extensive international cooperation network with more than 125 international education partners around the world including the United States, France, Australia, New Zealand, Netherlands, South Korea, Singapore, etc.
                </p>
              </div>
              <p data-aos="fade-up" data-aos-delay="200">
                <a
                  href="#features-section"
                  class="btn btn-primary smoothscroll"
                  style="margin-right: 5px"
                  :style="[
                    { background: themeColor },
                    { borderColor: themeColor },
                  ]"
                  >{{ buttonSeeFeature }}</a
                >
                <a
                  href="#pricing-section"
                  class="btn btn-outline-primary smoothscroll pricing"
                  :style="[{ color: themeColor }, { borderColor: themeColor }]"
                  >{{ buttonPricing }}</a
                >
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.pricing:hover {
  color: #fff !important;
}
</style>
