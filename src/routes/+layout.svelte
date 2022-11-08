<script lang="ts">
    import type { LayoutData } from './$types';
    import "../css/style.css"
    export let data: LayoutData;
</script>

<main>
    <slot></slot>
</main>