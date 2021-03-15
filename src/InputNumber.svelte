<script>
  export let min;
  export let max;
  export let step = 1;
  export let value = 0;
  export let label;
  export let sign;
</script>

<div class="input_number-block {$$props.class ? $$props.class : ''}">
  {#if label}<div class="mb-2">{label}</div>{/if}
  <span class="input_number-input_wrapper d-flex align-items-center">
    <input
      class="input_number-input"
      type="number"
      step={step}
      min={min}
      max={max}
      bind:value={value}
    >
    {#if sign}<span class="ml-3 text-nowrap">{sign}</span>{/if}
  </span>
</div>