<script setup>
import { themeColor } from "../data/items";
import personPhoto from "../assets/images/person_1.png";
import mainPhoto from "../assets/images/service3.jpg";

const service1Heading = "UEH OVERVIEW";
const service1SubHeading = "MISSION";
const service1Quote =
  '"UEH and its Member Colleges are commit to embrace the best practices of Esteemed Universities Worldwide."';
const personName = "Professor Su Dinh Thanh";
const designation = "President of UEH University";
function youtubeVideoUrl() {
  const youtubeVideoId = "urpvw6xvqco";
  return `https://www.youtube.com/watch?v=${youtubeVideoId}&amp;t=9s`;
}
</script>
<template>
  <div class="untree_co-section" id="features-section">
    <div class="container">
      <div class="row justify-content-between">
        <div class="col-lg-4">
          <span
            class="caption"
            data-aos="fade-up"
            data-aos-delay="0"
            :style="[{ color: themeColor }]"
            >{{ service1Heading }}</span
          >
          <h5 class="heading mb-4" data-aos="fade-up" data-aos-delay="100">
            {{ service1SubHeading }}
          </h5>
          <div class="mb-4" data-aos="fade-up" data-aos-delay="200">
            <p>
              
Along with the restructuring strategy of Ho Chi Minh City University of Economics, forming a multidisciplinary and sustainable UEH University in the period of 2021-2025 with a vision to 2030.
            </p>
            <ul class="list-unstyled ul-check primary">
              <li>Enhance Knowledge Acquisition</li>
              <li>Pioneer of Innovation & Creativity</li>
            </ul>
          </div>
          <div class="mb-4" data-aos="fade-up" data-aos-delay="300">
            <div class="untree_co-testimonial d-flex">
              <div class="text">
                <blockquote>
                  {{ service1Quote }}
                </blockquote>
                <div class="author d-flex">
                  <div class="pic mr-3">
                    <img :src="personPhoto" alt="Image" class="img-fluid" />
                  </div>
                  <div>
                    <strong class="d-block">{{ personName }}</strong
                    ><span class="d-block">{{ designation }}</span>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="col-lg-7" data-aos="fade-up" data-aos-delay="400">
          <a :href="youtubeVideoUrl()" class="btn-video" data-fancybox>
            <span class="wrap-icon-play">
              <svg
                class="bi bi-play-fill"
                width="1em"
                height="1em"
                viewBox="0 0 16 16"
                fill="currentColor"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path
                  d="M11.596 8.697l-6.363 3.692c-.54.313-1.233-.066-1.233-.697V4.308c0-.63.692-1.01 1.233-.696l6.363 3.692a.802.802 0 0 1 0 1.393z"
                />
              </svg>
            </span>
            <img :src="mainPhoto" alt="Image" class="img-fluid img-shadow" />
          </a>
        </div>
      </div>
    </div>
  </div>
</template>
