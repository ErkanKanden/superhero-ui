<template>
  <Page>
    <div class="tips-list">
      <div class="actions">
        <SendTip />
        <div class="not-bootstrap-row">
          <button
            :class="{ active: tipSortBy === 'hot' }"
            @click="setTipSortBy('hot')"
          >
            {{ $t('views.TipList.SortingMostPopular') }}
          </button>
          <button
            id="sort-latest"
            :class="{ active: tipSortBy === 'latest' }"
            @click="setTipSortBy('latest')"
          >
            {{ $t('views.TipList.SortingLatest') }}
          </button>
          <button
            :class="{ active: tipSortBy === 'highest' }"
            @click="setTipSortBy('highest')"
          >
            {{ $t('views.TipList.SortingHighestRated') }}
          </button>
          <div class="separator" />
          <ThreeDotsMenu>
            <Checkbox
              :checked="isHiddenContent"
              @change="setIsHiddenContent(!isHiddenContent)"
            >
              {{ $t('views.TipList.SafeContentOnly') }}
            </Checkbox>
          </ThreeDotsMenu>
        </div>
      </div>

      <TipsPagination
        :tip-sort-by="tipSortBy"
        :search="query"
        :blacklist="isHiddenContent"
      />
    </div>
  </Page>
</template>

<script>
import { mapState, mapMutations } from 'vuex';
import SendTip from '../components/layout/sendTip/SendTip.vue';
import Page from '../components/layout/Page.vue';
import TipsPagination from '../components/TipsPagination.vue';
import ThreeDotsMenu from '../components/ThreeDotsMenu.vue';
import Checkbox from '../components/Checkbox.vue';

export default {
  name: 'TipsList',
  components: {
    TipsPagination,
    Page,
    SendTip,
    Checkbox,
    ThreeDotsMenu,
  },
  props: {
    query: { type: String, default: '' },
  },
  computed: mapState(['tipSortBy', 'isHiddenContent']),
  methods: mapMutations(['setTipSortBy', 'setIsHiddenContent']),
};
</script>

<style lang="scss" scoped>
.tips-list .actions {
  position: sticky;
  top: 0;
  z-index: 100;
  font-size: 0.75rem;
  background-color: $background_color;
  color: $light_font_color;

  @include mobile {
    top: $mobile_navigation_height;
  }

  .send-tip {
    margin: 0.15rem 0;

    @include smallest {
      display: none;
    }
  }

  .not-bootstrap-row {
    background-color: $actions_ribbon_background_color;
    display: flex;
    align-items: center;
    padding: 0 1rem;

    @include smallest {
      background-color: $background_color;
      border-bottom: 0.075rem solid $search_nav_border_color;
      margin: 0 -1rem; // Would be better to reorganize layout somehow
    }

    button {
      background: none;
      border: none;
      outline: none;
      color: inherit;
      font-weight: 600;
      padding: 0.625rem 0;
      margin-left: 1rem;
      border-bottom: 0.1rem solid transparent;

      @include smallest {
        margin-left: 0;
        flex-grow: 1;
        flex-basis: 0;
        padding-bottom: 0.45rem;
        border-bottom-width: 0.075rem;
        margin-bottom: -0.075rem;
      }

      &:first-child {
        margin-left: 0;
      }

      &:hover {
        color: $primary_color;
      }

      &.active {
        color: $custom_links_color;
        border-bottom-color: $custom_links_color;
      }
    }

    .separator {
      flex-grow: 1;

      @include smallest {
        display: none;
      }
    }
  }
}
</style>
