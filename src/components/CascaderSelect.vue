<template>
  <div class="vcs" @keydown.esc="handleClose">
    <div class="vcs__picker" @click="() => handleOpen(false)" tabindex="0">
      <input disabled :value="value" :placeholder="placeholder" />

      <div class="vcs__arrow-container">
        <Arrow borderColor="#ccc" :direction="isOpen ? 'up' : 'down'" />
      </div>
    </div>
    <div v-if="isOpen" class="select-container">
      <div class="select-container__header">
        <button @click="log">Click</button>
      </div>
      <div class="select-container__footer">Footer</div>
      <SelectMenu ref="select-menu" :options="options" />
    </div>
  </div>
</template>

<script>
import Arrow from "./Arrow";
import SelectMenu from "./SelectMenu";

export default {
  name: "VueCascaderSelect",
  components: {
    Arrow,
    SelectMenu,
  },
  props: {
    placeholder: {
      type: String,
      default: "Please select...",
    },
    options: {
      type: Array,
      required: true,
    },
    value: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      isOpen: false,
      withKeyboard: false,
    };
  },
  methods: {
    handleSelect(option) {
      this.$emit("select", option);
    },
    handleOpen(withKeyboard = false) {
      this.isOpen = !this.isOpen;
      this.withKeyboard = withKeyboard;
    },
    handleClose() {
      this.isOpen = false;
    },
    log() {
      /* eslint-disable */
      let res = [];
      const rootMenu = this.$refs["select-menu"];
      for (let i = 1; i <= 4; i++) {
        debugger;
        let nextMenu = rootMenu.$refs.childMenu;
        if (nextMenu.selectedOptionIndex !== -1) {
          res = [
            ...res,
            {
              label: nextMenu.nextMenu.label,
              value: nextMenu.nextMenu.value,
            },
          ];
        } else {
          this.res = [];
          break;
        }
      }
      console.log(res);
    },
  },
  watch: {
    value() {
      this.isOpen = false;
    },
  },
};
</script>

<style>
button {
  padding: 0;
  background: none;
  border: none;
  text-align: left;
  font-size: unset;
}

.vcs {
  position: relative;
}

.vcs__picker {
  position: relative;
  display: flex;
  width: 100%;
}

.vcs__picker input {
  align-items: center;
  border-radius: 4px;
  border: 1px solid #ccc;
  box-shadow: none;
  cursor: pointer;
  display: flex;
  flex-direction: row;
  font-size: inherit;
  height: 30px;
  justify-content: space-between;
  overflow: hidden;
  padding: 0 55px 0 10px;
  text-align: center;
  text-align: left;
  text-overflow: ellipsis;
  user-select: none;
  white-space: nowrap;
  width: 100%;
  -webkit-appearance: none;
}

.vcs__picker input:disabled {
  background: inherit;
  opacity: 1;
}

.vcs__arrow-container {
  border-left: 1px solid #ccc;
  cursor: pointer;
  padding-left: 10px;
  margin-left: 10px;
  position: absolute;
  right: 11px;
  top: 50%;
  transform: translate(0, -50%);
}

.select-container {
  border-radius: 4px;
  margin-top: 2px;
  padding: 5px 0;
  position: relative;
  text-align: left;
  width: 100%;
  min-width: 150px;
  background: white;
  position: absolute;
  left: 0;
  top: calc(100% + 2px);
  margin-top: 0;
}

.vcs__fade-enter-active,
.vcs__fade-leave-active {
  transition: opacity 0.2s;
}

.vcs__fade-enter,
.vcs__fade-leave-to {
  opacity: 0;
}
</style>
