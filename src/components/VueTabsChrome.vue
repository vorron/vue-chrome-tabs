<script setup lang="ts">
export interface Tab {
  label: string
  key: string
  favicon: string
}

defineProps<{ tabs: Tab[] }>()
const tabKey = defineModel<string>('modelValue', { required: true })
const emit = defineEmits<{
  close: [value: string]
  activate: [value: string]
}>()

const onClick = (value: string) => {
  tabKey.value = value
  emit('activate', value)
}

const onClose = (value: string) => {
  if (tabKey.value === value) tabKey.value = ''
  emit('close', value)
}

const speed = '150ms'
</script>

<template>
  <div class="tabs-chrome">
    <div class="tabs">
      <div
        class="tab"
        v-for="tab in tabs"
        :class="{ active: tab.key === tabKey }"
        :key="tab.key"
        @click="onClick(tab.key)"
      >
        <img class="img" :src="tab.favicon" alt="" />
        <div class="label">{{ tab.label }}</div>
        <div class="close" @click.stop="onClose(tab.key)">
          <svg class="close-icon" width="16" height="16" stroke="#595959">
            <path d="M 4 4 L 12 12 M 12 4 L 4 12"></path>
          </svg>
        </div>
        <svg class="bottom-radius-before" width="7" height="7">
          <path d="M 0 7 A 7 7 0 0 0 7 0 L 7 7 Z"></path>
        </svg>
        <svg class="bottom-radius-after" width="7" height="7">
          <path d="M 0 0 A 7 7 0 0 0 7 7 L 0 7 Z"></path>
        </svg>
      </div>
    </div>
  </div>
</template>

<style scoped>
.tabs-chrome {
  padding-top: 10px;
  background-color: #dee1e6;
}
.tabs {
  height: 34px;
  display: flex;
}

.tab {
  border-top-left-radius: 5px;
  border-top-right-radius: 5px;
  transition: 150ms;
  display: flex;
  align-items: center;
  min-width: 2.5in;
  cursor: pointer;
  position: relative;
  z-index: 1;
  user-select: none;

  &:first-of-type {
    margin-left: 8px;
  }

  &:first-of-type::before {
    display: none;
  }

  &:last-of-type::after {
    background-color: #81878c;
    bottom: 25%;
    content: '';
    height: 60%;
    top: 20%;
    width: 1px;
  }

  &:hover {
    background-color: #f2f3f5;
    z-index: 3;
    & + .tab::before {
      display: none;
    }
    &::before {
      display: none;
    }
    &::after {
      display: none;
    }
    & .bottom-radius-before {
      fill: #f2f3f5;
      z-index: 3;
    }
    & .bottom-radius-after {
      fill: #f2f3f5;
      z-index: 3;
    }
  }
  &.active {
    background-color: #fff;
    z-index: 5;
    & + .tab::before {
      display: none;
    }
    &::before {
      display: none;
    }
    &::before {
      display: none;
    }
    &::after {
      display: none;
    }
    & .bottom-radius-before {
      fill: #fff;
      z-index: 5;
    }
    & .bottom-radius-after {
      fill: #fff;
      z-index: 5;
    }
  }
}

.tab::before {
  background-color: #81878c;
  bottom: 25%;
  content: '';
  height: 60%;
  top: 20%;
  width: 1px;
}

.img {
  height: 20px;
  margin-left: 3%;
  flex-grow: 0;
}

.label {
  flex-grow: 1;
  margin-left: 5px;
}

.close {
  width: 16px;
  height: 16px;
  flex-grow: 0;
  margin-right: 5px;
}

.close-icon {
  width: 100%;
  height: 100%;
  border-radius: 50%;

  &:hover {
    stroke: #000;
    background-color: #e8eaed;
  }
}

.bottom-radius-before,
.bottom-radius-after {
  bottom: -0px;
  position: absolute;
  fill: transparent;
  transition: v-bind(speed);
}

.bottom-radius-before {
  left: -7px;
}

.bottom-radius-after {
  right: -7px;
}
</style>
