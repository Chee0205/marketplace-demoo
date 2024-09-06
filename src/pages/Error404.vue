<script>
import PageComponentMixin from 'src/mixins/pageComponent'

export default {
  mixins: [
    PageComponentMixin,
  ],
  data() {
    return {
      errorCode: 404 // Default error code
    }
  },
  beforeMount() {
    // Extract the last 3-digit number from the URL, default to 404 if not found
    const match = this.$route.path.match(/(\d{3})$/);
    if (match) {
      this.errorCode = parseInt(match[1], 10);
    }
  }
}
</script>

<template>
  <QPage class="flex flex-center">
    <div class="text-center">
      <!-- Header for the Not Found page -->
      <AppContent
        class="text-h5 text-weight-medium"
        tag="h1"
        entry="pages"
        field="not_found.header"
      />

      <!-- Button to redirect to the home page -->
      <QBtn
        class="q-mb-xl"
        color="secondary"
        :to="{ name: 'home' }"
        :label="$t({ id: 'navigation.home' })"
      />

      <!-- Error message display -->
      <p
        v-if="errorCode === 404"
        class="text-grey"
      >
        {{ $t({ id: 'pages.not_found.404_error_label' }) }}
      </p>
      <p
        v-else
        class="text-grey"
      >
        <AppContent
          entry="pages"
          field="not_found.custom_error_code_label"
          :options="{ errorCode }"
        />
      </p>
    </div>
  </QPage>
</template>
