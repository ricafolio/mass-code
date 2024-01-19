<template>
  <PerfectScrollbar>
    <div class="fragments">
      <div
        v-for="(i, index) in snippetStore.fragmentLabels"
        :key="index"
        class="item"
        :class="{ 'is-active': index == snippetStore.fragment }"
        @click="onClickFragment(index)"
      >
        <SnippetsFragmentsInput
          :name="i"
          :index="index"
        />
      </div>
    </div>
  </PerfectScrollbar>
</template>

<script setup lang="ts">
import { useAppStore } from '@/store/app'
import { useSnippetStore } from '@/store/snippets'

const snippetStore = useSnippetStore()
const appStore = useAppStore()

const onClickFragment = (index: number) => {
  snippetStore.fragment = index
}

const fragmentHeight = appStore.sizes.editor.fragmentsHeight + 'px'
</script>

<style lang="scss" scoped>
.fragments {
  display: flex;
  align-items: center;
  height: v-bind(fragmentHeight);
  margin: 4px 8px 0;
  /* // overflow-y: auto; */
  .item {
    cursor: pointer;
    padding: 0 calc(var(--spacing-xs) + 4px);
    margin-right: 2px;
    display: flex;
    align-items: center;
    height: v-bind(fragmentHeight);
    width: 100%;
    border-radius: 8px 8px 0 0;
    min-width: 100px;
    &:last-child {
      margin-right: 0;
    }
    &.is-active {
      background-color: var(--color-bg-editor);
    }
  }
}
</style>
