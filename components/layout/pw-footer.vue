<template>
  <footer class="flex-col flex-no-wrap">
    <div class="row-wrapper">
      <span v-if="version.name" class="font-mono"> Версия:{{ version.name }} </span>
      <span>
        <v-popover>
          <button class="icon" v-tooltip="$t('choose_language')">
            <i class="material-icons">translate</i>
          </button>
          <template slot="popover">
            <div v-for="locale in availableLocales" :key="locale.code">
              <nuxt-link :to="switchLocalePath(locale.code)">
                <button class="icon" v-close-popover>
                  {{ locale.name }}
                </button>
              </nuxt-link>
            </div>
          </template>
        </v-popover>
      </span>
    </div>
  </footer>
</template>

<style scoped lang="scss">
.footer-link {
  @apply my-2;
  @apply mx-4;
  @apply text-fgLightColor;

  &:hover {
    @apply text-fgColor;
  }
}
</style>

<script>
import * as version from "../../.hoppscotch/version.json"

export default {
  data() {
    return {
      version: {},
    }
  },

  beforeMount() {
    // Set version data
    this.version = version.default
  },

  computed: {
    availableLocales() {
      return this.$i18n.locales.filter(({ code }) => code !== this.$i18n.locale)
    },
  },
}
</script>
