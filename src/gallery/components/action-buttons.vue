<template>
  <div class="action-container">
    <group-buttons :actions="SECTIONS" v-model="filtersData.selectedSection"/>
    <group-buttons
      :actions="SORTS"
      v-model="filtersData.selectedSort"
      v-if="filtersData.selectedSection === 'user'"
    />
    <group-buttons
      v-else-if="filtersData.selectedSection === 'top'"
      :actions="WINDOWS"
      v-model="filtersData.selectedWindow"
    />
    <switch-input
      v-model="filtersData.showViral"
      title="show viral"
      v-if="filtersData.selectedSection === 'user'"
    />
  </div>
</template>

<script>
import { SECTIONS, SORTS, WINDOWS, SECTIONS_DEFAULT,
 SORTS_DEFAULT, WINDOWS_DEFAULT } from '@/gallery/constants/gallery.constant';
import GroupButtons from '@/components/group-buttons';
import SwitchInput from '@/components/switch';

export default {
  name: 'SectionButtons',
  components: {
    GroupButtons,
    SwitchInput,
  },
  data() {
    return {
      SECTIONS,
      SORTS,
      WINDOWS,
      filtersData: {
        selectedSection: SECTIONS_DEFAULT,
        selectedSort: SORTS_DEFAULT,
        selectedWindow: WINDOWS_DEFAULT,
        showViral: true
      }
    };
  },
  watch: {
    filtersData: {
      handler(newValue) {
        this.$store.commit('galleryStore/setFiltersData', newValue);
        this.$store.dispatch('galleryStore/getGalleryItems');
      },
      deep: true
    }
  }
};
</script>

<style lang="scss" scoped>
@import "~@/assets/scss/_variables.scss";

.action-container {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  position: sticky;
  top: 60px;
  margin: 50px auto;
  background: $secondaryColor;
  z-index: 1;
  padding: 10px 60px;
}
@media screen and (max-width: 600px) {
  .action-container {
    margin: 10px auto;
    padding: 10px;
  }
  .btn-group {
    margin: 5px auto;
  }
}
</style>
