<script>
    import ResetItems from '$lib/components/reset-items.svelte'
    import HeaderBrand from '@nick-mazuk/ui-svelte/src/components/header/header-brand/header-brand.svelte'
    import HeaderLink from '@nick-mazuk/ui-svelte/src/components/header/header-link/header-link.svelte'
    import HeaderMobileLink from '@nick-mazuk/ui-svelte/src/components/header/header-mobile-link/header-mobile-link.svelte'
    import Header from '@nick-mazuk/ui-svelte/src/components/header/header.svelte'
</script>

<ResetItems />

<Header sticky>
    <HeaderBrand text="{import.meta.env.VITE_PUBLIC_SITE_NAME}" slot="left" />
    <svelte:fragment slot="right">
        <HeaderLink href="https://nickmazuk.com">About Nick</HeaderLink>
    </svelte:fragment>
    <svelte:fragment slot="mobile">
        <HeaderMobileLink href="https://nickmazuk.com">About Nick</HeaderMobileLink>
    </svelte:fragment>
</Header>
<slot />
