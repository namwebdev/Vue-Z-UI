<template>
  <div
    class="vcs__select-menu"
    :class="{ 'vcs__select-menu__not-main': notMain }"
  >
    <Option
      v-for="(option, index) in options"
      :index="index"
      ref="options"
      :key="option.value"
      :option="option"
      :active="selectedOptionIndex === index"
      @on-select="handleOpenNextMenu"
    />

    <transition name="vcs__fade">
      <SelectMenu
        ref="childMenu"
        v-if="nextMenu.isOpen"
        :notMain="true"
        :options="nextMenu.options"
      />
    </transition>
  </div>
</template>

<script>
import Option from "./Option.vue";

export default {
  name: "SelectMenu",
  components: { Option },
  props: {
    notMain: {
      type: Boolean,
      default: false,
    },
    options: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    const { options } = this.$props;

    return {
      nextMenu: {
        isOpen: false,
        options: false,
        value: "",
        label: "",
      },
      selectedOptionIndex: -1,
      optionsLength: options.length,
    };
  },
  methods: {
    handleOpenNextMenu(selectedOption, index) {
      const options = { selectedOption };
      this.selectedOptionIndex = index;
      this.nextMenu = {
        options: selectedOption.options,
        isOpen: !!selectedOption.options,
        value: selectedOption.value,
        label: selectedOption.label,
      };
      this.$refs.options[index].$el.focus();

      if (options && this.$refs.childMenu) {
        this.$refs.childMenu.resetNextMenu();
      }

      if (!options) {
        this.resetNextMenu();
      }
      this.$nextTick(() => {});
    },
    resetNextMenu() {
      this.nextMenu = {
        isOpen: false,
        options: [],
        value: "",
      };
      this.selectedOptionIndex = -1;
    },
    handleCloseMenu() {
      if (this.$parent && this.$parent.resetNextMenu) {
        this.$parent.resetNextMenu();
      }
    },
  },
};
</script>

<style>
.vcs__select-menu {
  border-radius: 4px;
  border: 1px solid #ccc;
  display: flex;
  flex-direction: column;
  margin-top: 2px;
  padding: 5px 0;
  position: relative;
  text-align: left;
  width: 25%;
  min-width: 150px;
  background: white;
  margin-top: 0;
}

.vcs__select-menu__not-main {
  position: absolute;
  left: calc(100% - 1px);
  top: -1px;
  margin-top: 0;
  width: auto;
}
</style>
