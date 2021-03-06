<template>
  <div>
    <action-buttons/>
    <div class="gallery" infinite-scroll-distance="800" v-infinite-scroll="loadMore">
      <router-link
        :to="{name: 'img-details', params: { id: galleryImage.id, galleryImage }}"
        class="gallery__item"
        v-for="galleryImage in displayedGalleryImages"
        :key="galleryImage.id"
        :title="galleryImage.title"
        tabindex="0"
      >
        <figure>
          <img
            class="gallery__item__img lazy"
            :data-src="galleryImage.smallImage"
            src="/img/loading.svg"
            :alt="galleryImage.title || 'image'"
          >
          <figcaption class="gallery__item__caption">{{galleryImage.title || 'image'}}</figcaption>
        </figure>
      </router-link>
    </div>
  </div>
</template>

<script>

import { mapState } from 'vuex';
import ActionButtons from '@/gallery/components/action-buttons';

export default {
  name: 'Gallery',
  components: {
    ActionButtons,
  },
  data() {
    return {
      displayedGalleryImages: []
    };
  },
  computed: {
    ...mapState({
      galleryImages: state => state.galleryStore.galleryImages,
    })
  },
  mounted() {
    window.scrollTo(0, 0);
    window.addEventListener("scroll", this.lazyLoad);
  },
  methods: {
    loadMore() {
      const startIndex = this.displayedGalleryImages.length;
      this.displayedGalleryImages.push(
        ...this.galleryImages.slice(startIndex, startIndex + 8)
      );
      return this.displayedGalleryImages;
    },
    lazyLoad () {
    let lazyImages = [].slice.call(document.querySelectorAll("img.gallery__item__img"));
    let active = false;
    if (active === false) {
      active = true;
      setTimeout(() => {
        lazyImages.forEach(function (lazyImage) {
          if ((lazyImage.getBoundingClientRect().top <= window.innerHeight && lazyImage.getBoundingClientRect().bottom >= 0) && getComputedStyle(lazyImage).display !== "none") {
            lazyImage.src = lazyImage.dataset.src;
            lazyImage.classList.remove("lazy");
            lazyImages = lazyImages.filter(function (image) {
              return image !== lazyImage;
            });

            if (lazyImages.length === 0) {
              window.removeEventListener('scroll', this.lazyLoad);
            }
          }
        });
        active = false;
      }, 200);
     }
    },
  },
  created() {
    if (!this.galleryImages.length) {
      this.$store.dispatch('galleryStore/getGalleryItems');
    }
  },
  watch: {
    galleryImages(galleryImages) {
      if (galleryImages.length) {
        this.displayedGalleryImages = galleryImages.slice(0, 8);
      }
    }
  },
};

</script>

<style lang="scss" scoped>
@import "~@/assets/scss/_variables.scss";

*,
*:before,
*:after {
  box-sizing: border-box;
}
figure {
  margin-block-start: 0;
  margin-block-end: 0;
  margin-inline-start: 0;
  margin-inline-end: 0;
}
.lazy {
  filter: blur(4px);
}
.gallery {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  grid-gap: 1rem;
  margin: 0 4rem;
  &__item {
    box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
    transition: 0.3s;
    position: relative;
    cursor: pointer;
    &:hover {
      box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.2);
    }
    &:hover .gallery__item__caption {
      opacity: 1;
    }
    &__img {
      max-width: 100%;
      object-fit: cover;
      height: 300px;
      object-position: top;
      width: 400px;
    }
    &__caption {
      position: absolute;
      bottom: 0;
      background: rgb(0, 0, 0);
      background: rgba(0, 0, 0, 0.5); /* Black see-through */
      width: 100%;
      transition: 0.5s ease;
      opacity: 0;
      color: $secondaryColor;
      padding: 10px;
      text-align: center;
    }
  }
}

@media screen and (max-width: 600px) {
  .gallery {
    margin: 0 15px;
    &__item {
      &__img {
        width: none;
      }
    }
  }
}
</style>
