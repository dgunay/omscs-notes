<template lang="html">
  <div class="ActiveSidebarLink">
    <a href="#" @click.prevent="expanded = !expanded">
      <div class="flex text-gray-700">
        <div class="mr-1 flex items-center" v-if="collapsible">
          <i v-if="expanded" class="fas fa-minus fa-xs" />
          <i v-else class="fas fa-plus fa-xs" />
        </div>
        <p class="font-bold leading-tight">
          {{ note.title }}
        </p>
      </div>
    </a>
    <ul v-if="expanded || !collapsible">
      <li v-for="({ value, depth, anchor }, i) in headings" :key="i">
        <a
          :href="anchor"
          class="block text-gray-600 text-sm"
          :style="{ paddingLeft: `${(depth - 1) * 16}px` }"
          >{{ value }}</a
        >
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'ActiveSidebarLink',

  props: {
    note: {
      type: Object,
      required: true,
    },
  },

  data() {
    return {
      expanded: false,
      collapsible: true,
    }
  },

  mounted() {
    if (this.note.lecture === 'welcome') {
      this.collapsible = false
    }
  },

  computed: {
    headings() {
      return this.note.headings.filter(
        (heading) => heading.depth === 2 || heading.depth === 3
      )
    },
  },
}
</script>
