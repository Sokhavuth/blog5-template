<script>
    import Layout from "$lib/components/Layout.svelte"
    import Latest from '$lib/components/Latest.svelte'
    let { data } = $props()
</script>

<Layout {data}>
<section class="Index region">
    <Latest {data} />
</section>
</Layout>