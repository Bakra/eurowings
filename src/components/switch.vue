<template>
  <div class="switch__input">
    <label for="switch" class="switch__input__title">{{title}}</label>
    <label class="switch" :title="title">
      <input
        aria-label="switch"
        id="switch"
        v-bind="$attrs"
        @click="$emit('checked', !showViral)"
        type="checkbox"
      >
      <span tabindex="0" class="slider round"></span>
    </label>
  </div>
</template>

<script>
export default {
  name: 'GroupButtons',
  inheritAttrs: false,
  model: {
    prop: 'showViral',
    event: 'checked',
  },
  props: {
    showViral: {
      type: Boolean,
      required: true
    },
    title: {
      type: String,
    }
  },
};
</script>

<style lang="scss" scoped>
.switch__input {
  display: flex;
  align-items: center;
  &__title {
    color: #66cc00;
    font-size: 16px;
  }
}
.switch {
  position: relative;
  display: inline-block;
  width: 60px;
  height: 34px;
  margin-left: 10px;
}

.switch input {
  opacity: 0;
  width: 0;
  height: 0;
}

.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #ccc;
  -webkit-transition: 0.4s;
  transition: 0.4s;
}

.slider:before {
  position: absolute;
  content: "";
  height: 26px;
  width: 26px;
  left: 4px;
  bottom: 4px;
  background-color: white;
  -webkit-transition: 0.4s;
  transition: 0.4s;
}

input:checked + .slider {
  background-color: #66cc00;
}

input:focus + .slider {
  box-shadow: 0 0 1px #66cc00;
}

input:checked + .slider:before {
  -webkit-transform: translateX(26px);
  -ms-transform: translateX(26px);
  transform: translateX(26px);
}

/* Rounded sliders */
.slider.round {
  border-radius: 34px;
}

.slider.round:before {
  border-radius: 50%;
}
</style>
