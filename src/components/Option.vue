<template>
  <button
    class="vcs__option"
    :class="{
      'vcs__option--active': active,
      'vcs__option--disabled': disabled,
      'vsc__option--focused': focused,
    }"
    @click="handleSelection"
  >
    <span>{{ option.label }}</span>
    <arrow v-if="!isLeaf" direction="right" />
  </button>
</template>

<script>
import Arrow from "./Arrow.vue";

export default {
  name: "Option",
  components: { Arrow },
  props: {
    active: {
      type: Boolean,
      default: false,
    },
    option: { type: Object },
    value: {
      type: [String, Number],
    },
    selectable: {
      type: Boolean,
      default: true,
    },
    disabled: {
      type: Boolean,
      default: false,
    },
    focused: {
      type: Boolean,
      default: false,
    },
    index: [Number, String],
  },
  methods: {
    handleSelection() {
      if (this.selectable && !this.disabled) {
        this.$emit("on-select", this.option, this.index);
      }
    },
  },
  computed: {
    isLeaf() {
      return (this.option.options || []).length === 0;
    },
  },
};
</script>

<style>
.vcs__option {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  padding: 5px 10px;
  cursor: pointer;
  transition: background 200ms linear;

  /* Normalize button */
  color: inherit;
  font-family: inherit;
  font-size: 100%;
  line-height: 1.15;
  overflow: visible;
  -webkit-appearance: button;
}

.vcs__option--active {
  background-color: #eee;
}

.vcs__option span {
  width: 100%;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  margin-right: 10px;
}

.vcs__option:focus {
  outline: none;
}

.vsc__option--focused {
  background: #ddd;
  outline: none;
}
</style>
