<script lang="ts">
    import Button from '@smui/button';

	const light_css = "/smui.css";
	const dark_css = "/smui-dark.css";

	let dark_mode: boolean | undefined = undefined;

    enum Calculator {
		AscendingAorta,
		Thymus,
		DoublingTime
	}

    let active_calculator = $state(Calculator.AscendingAorta);
</script>

<svelte:head>
    <!-- If dark mode is undefined, use user preference -->
	{#if dark_mode === undefined}
		<link rel="stylesheet" href={light_css} media="(prefers-color-scheme: light)" />
		<link rel="stylesheet" href={dark_css} media="screen and (prefers-color-scheme: dark)" />
	{:else if dark_mode}
    <!-- If dark mode is defined, overried user preference -->
		<link rel="stylesheet" href={light_css} media="print" />
		<link rel="stylesheet" href={dark_css} media="screen" />
	{:else}
		<link rel="stylesheet" href={light_css} />
	{/if}
</svelte:head>



<div class="main">
    <div class="header">
        <h1>
            RadCalc
        </h1>
        <div class="top_bar_button_section">
            <Button variant="raised" color={active_calculator==Calculator.AscendingAorta ? "primary" : "secondary"}
                onclick={()=>{active_calculator=Calculator.AscendingAorta; console.debug("AscendingAorta");}}
            >
                Ascending Aorta
            </Button>
            <Button variant="raised" color={active_calculator==Calculator.DoublingTime ? "primary" : "secondary"}
                onclick={()=>{active_calculator=Calculator.DoublingTime; console.debug("DoublingTime");}}
            >
                Doubling Time
            </Button>
            <Button variant="raised" color={active_calculator==Calculator.Thymus ? "primary" : "secondary"}
                onclick={()=>{active_calculator=Calculator.Thymus; console.debug("Thymus");}}
            >
                Thymic SII/CSR
            </Button>
        </div>
    </div>
    <div class="calculator">
        {#if active_calculator === Calculator.AscendingAorta}
            AAo
        {:else if active_calculator === Calculator.DoublingTime}
            DT
        {:else if active_calculator === Calculator.Thymus}
            Thy
        {/if}
    </div>
    <div class="footer">
        Footer
    </div>
</div>

<style>
  /* Hide everything above this component. */
  :global(#smui-app),
  :global(body),
  :global(html) {
    display: block !important;
    height: auto !important;
    width: auto !important;
    position: static !important;
  }

  .header {
    width: 100%;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
  }

  .top_bar_button_section {
    width: 100%;
    display: flex;
    flex-direction: row;
    justify-content: space-around;
  }

  .main {
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: start;
    flex-grow: 1;
  }

  .calculator {
    width: 100%;
    flex-grow: 1;
  }

  .footer {
    width: 100%;
    flex-shrink: 1;
  }
</style>