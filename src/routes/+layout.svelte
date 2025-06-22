<script lang="ts">
    let { children } = $props();

    import "@fontsource/roboto"; //Needed by material UI.
    import "./font.scss"; //Needed by materialUI
</script>

{@render children()}