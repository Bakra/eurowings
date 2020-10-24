<template>
  <div class="image-wrapper">
    <div class="image">
      <h2 class="image__title">{{imageDetails.title}}</h2>
      <figure>
        <img class="image__img" :src="imageDetails.bigImage" :alt="imageDetails.title">
        <figcaption class="image__caption">{{imageDetails.title}}</figcaption>
      </figure>
      <div class="image__details">
        <p class="image__details__description">{{imageDetails.description}}</p>
      </div>
      <div class="image__analytics">
        <div class="image__analytics__item">
          <img src="/img/upvote.png" alt="upvotes" class="image__analytics__item__icons"  />
          <span>{{imageDetails.ups}}</span>
        </div>
        <div class="image__analytics__item">
          <img src="/img/downvote.png" alt="downvotes" class="image__analytics__item__icons"  />
          <span>{{imageDetails.downs}}</span>
        </div>
        <div class="image__analytics__item">
          <img src="/img/star.png" alt="star" class="image__analytics__item__icons"  />
          <span>{{imageDetails.score}}</span>
        </div>
        <div class="image__analytics__item">
          <img src="/img/eye.png" alt="eye" class="image__analytics__item__icons"  />
          <span>{{imageDetails.views}}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'GalleryImgDetails',
  props: {
    galleryImage: {
      type: Object,
      default: () => {},
    },
    id: {
      type: String,
      required: true
    }
  },
  computed: {
    imageDetails() {
      return this.galleryImage || this.$store.state.galleryStore.imgDetails;
    }
  },
  created() {
    if (!this.galleryImage) {
      this.$store.dispatch('galleryStore/getGalleryImageDetails', this.id);
    }
  }
};
</script>

<style lang="scss" scoped>
@import "~@/assets/scss/_variables.scss";
.image-wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 5px;
}
.image {
  // border: 1px solid $primaryColor;
  max-width: 800px;
  margin: 40px auto;
  &__title {
    text-align: justify;
    font-size: 18px;
    padding: 4px;
  }
  &__img {
    display: block;
    max-width: 100%;
    object-fit: cover;
    object-position: top;
    margin: auto;
  }
  &__caption {
    text-align: center;
    padding: 10px;
  }
  &__details {
    &__description {
      text-align: justify;
      padding: 5px;
    }
  }
  &__analytics {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-evenly;
    align-items: center;
    padding: 10px;
    border-top: 1px dashed $primaryColor;
    &__item {
      display: flex;
      justify-content: center;
      margin: 3px 5px;
      align-items: center;
      &__icons {
        height: 32px;
        width: 32px;
        margin-right: 5px;
      }
    }
  }
}
</style>
