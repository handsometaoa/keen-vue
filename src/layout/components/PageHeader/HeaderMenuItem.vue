<template>
  <div
    class="menu-item menu-lg-down-accordion menu-sub-lg-down-indention me-0 me-lg-2"
    :class="{' menu-dropdown  show': hover}"
    @mouseenter="hover = true"
    @mouseleave="hover = false"
  >
    <router-link
      ref="tag"
      :key="realMenu(route).path"
      tag="span"
      class="menu-link"
      :to="{ path: realMenu(route).path, fullPath: realMenu(route).fullPath }"
    >

      <span
        v-if="route.parentId"
        class="menu-link-icon"
      >
        <span
          v-if="route.meta.icon"
          class="menu-icon"
        >
          <i
            class="fs-3 "
            :class="route.meta.icon"
          />
        </span>
        <span
          v-else
          class="menu-bullet"
        >
          <span class="bullet bullet-dot" />
        </span>
      </span>

      <span class="menu-title">{{ realMenu(route).meta.title }}</span>
      <span
        v-if="hasChild(route.children) && route.parentId"
        class="menu-arrow"
      />
    </router-link>
    <div
      v-if="route.id && hasChild(route.children)"
      class="menu-sub menu-sub-lg-down-accordion menu-sub-lg-dropdown px-lg-2 py-lg-4 w-lg-200px"
      :class="menuSubCls(route)"
    >
      <header-menu-item
        v-for="(subMenu, index) in route.children"
        :key="index"
        :route="subMenu"
        v-on="$listeners"
      />
    </div>
  </div>
</template>
<script>
export default {
  name: 'HeaderMenuItem',
  props: {
    route: {
      type: Object,
      default() {
        return {}
      }
    }
  },
  data() {
    return {
      hover: false
    }
  },
  created() {
    this.$watch(
      () => this.route.hover,
      () => {
        this.hover = this.route.hover
      }
    )
  },
  methods: {
    realMenu(menu) {
      if (menu.id) {
        return menu
      }
      return menu.children[0]
    },
    hasChild(children = []) {
      if (children.length > 0) {
        return true
      }
      return false
    },
    menuSubCls(route) {
      return !route.parentId ? 'show fixed-show' : 'show abs-show'
    }
  }
}
</script>
<style lang="scss" scoped>
.fixed-show {
    position: fixed;

    top: 70px;
}

.abs-show {
    position: absolute;
    transform: translate(180px, -35px);
}
</style>
