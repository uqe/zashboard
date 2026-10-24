<template>
  <div
    class="relative flex size-full flex-col overflow-hidden"
    :style="!isConnectionCard && padding"
  >
    <template v-if="isConnectionCard">
      <ConnectionCardList />
    </template>
    <template v-else>
      <ConnectionCtrl />
      <ConnectionTable />
    </template>
    <ConnectionDetails />
  </div>
</template>

<script setup lang="ts">
import ConnectionCardList from '@/components/connections/ConnectionCardList.vue'
import ConnectionDetails from '@/components/connections/ConnectionDetails.vue'
import ConnectionTable from '@/components/connections/ConnectionTable.vue'
import ConnectionCtrl from '@/components/controls/ConnectionCtrl.tsx'
import { usePaddingForViews } from '@/composables/paddingViews'
import { isConnectionCard } from '@/store/settings'
import { showConnectionTimestamp } from '@/store/connections'
import { useHotkeys } from '@tanstack/vue-hotkeys'

const toggleConnectionTimeFormat = () => {
  showConnectionTimestamp.value = !showConnectionTimestamp.value
}

useHotkeys(
  [
    { hotkey: { key: 'R' }, callback: toggleConnectionTimeFormat },
    { hotkey: { key: 'R', shift: true }, callback: toggleConnectionTimeFormat },
    { hotkey: { key: 'К' }, callback: toggleConnectionTimeFormat },
    { hotkey: { key: 'К', shift: true }, callback: toggleConnectionTimeFormat },
  ],
  {
    requireReset: true,
    meta: {
      name: 'Toggle connection time format',
      description: 'Switch Connect Time between relative time and timestamp',
    },
  },
)

const { padding } = usePaddingForViews({
  offsetTop: 0,
  offsetBottom: 0,
})
</script>

<style>
.vjs-tree {
  font-family:
    NotoEmoji,
    Monaco,
    Menlo,
    Consolas,
    Bitstream Vera Sans Mono,
    monospace;
}
.vjs-tree-node.is-highlight,
.vjs-tree-node:hover {
  background-color: var(--color-base-200);
}
</style>
