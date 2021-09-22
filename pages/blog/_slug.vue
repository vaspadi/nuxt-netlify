<template>
  <NuxtContent :document="page" />
</template>

<script>

export default {

  async asyncData ({ $content, params, error }) {
    const slug = params.slug || 'index'
    const page = await $content(`blog/${slug}`)
      .sortBy('createdAt', 'asc')
      .fetch()
      .catch(() => {
        error({ statusCode: 404, message: 'Page not found' })
      })

    return {
      page
    }
  }
}
</script>

<style scoped>

</style>
