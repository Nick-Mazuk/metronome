<script lang="ts">
    import Metronome from '$lib/components/metronome/metronome.svelte'
    import Seo from '@nick-mazuk/ui-svelte/src/utilities/seo/seo.svelte'
</script>

<Seo title="" siteName="{import.meta.env.VITE_PUBLIC_SITE_NAME}" />

<main id="main-content" class="wrapper pt-6">
    <Metronome />
</main>
