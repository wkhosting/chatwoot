<template>
  <div class="relative">
    <div class="flex px-4 pb-1 pt-2.5 border-b border-transparent">
      <woot-sidemenu-icon
        size="tiny"
        class="relative top-0 left-[-6px] rtl:left-0 rtl:right-[-6px]"
      />
      <router-link
        :to="searchUrl"
        class="search-link flex-1 items-center gap-1 text-left mr-1 rtl:mr-0 rtl:ml-1 h-6 rtl:text-right rounded-md px-2 py-0 bg-slate-25 dark:bg-slate-800 inline-flex"
      >
        <div class="flex">
          <fluent-icon
            icon="search"
            class="search--icon text-slate-800 dark:text-slate-200"
            size="16"
          />
        </div>
        <p
          class="search--label mb-0 overflow-hidden whitespace-nowrap text-ellipsis text-sm text-slate-800 dark:text-slate-200"
        >
          {{ $t('CONVERSATION.SEARCH_MESSAGES') }}
        </p>
      </router-link>
      <switch-layout
        :is-on-expanded-layout="isOnExpandedLayout"
        @toggle="$emit('toggle-conversation-layout')"
      />
    </div>
  </div>
</template>

<script>
import { mixin as clickaway } from 'vue-clickaway';
import { mapGetters } from 'vuex';
import timeMixin from '../../../../mixins/time';
import messageFormatterMixin from 'shared/mixins/messageFormatterMixin';
import SwitchLayout from './SwitchLayout.vue';
import { frontendURL } from 'dashboard/helper/URLHelper';
export default {
  components: {
    SwitchLayout,
  },
  directives: {
    focus: {
      inserted(el) {
        el.focus();
      },
    },
  },
  mixins: [timeMixin, messageFormatterMixin, clickaway],
  props: {
    isOnExpandedLayout: {
      type: Boolean,
      required: true,
    },
  },

  computed: {
    ...mapGetters({
      accountId: 'getCurrentAccountId',
    }),
    searchUrl() {
      return frontendURL(`accounts/${this.accountId}/search`);
    },
  },
};
</script>
<style lang="scss" scoped>
.search-link {
  &:hover {
    .search--icon,
    .search--label {
      @apply hover:text-woot-500 dark:hover:text-woot-500;
    }
  }
}
</style>
