<script>
  import InputNumber from "./InputNumber.svelte";

  const FULL_LVL = "full";
  const PART_LVL = "part";
  const CUSTOM_LVL = "custom";

  let level = FULL_LVL;
  let hours = 0;
  let reservDays;
  let reservLevel;
  $: reservLevel = Number(getReservLevel(level, hours, reservDays).toFixed(2));

  function getReservLevel() {
    switch (level) {
      case FULL_LVL:
        return reservDays * 1.3;
      case PART_LVL:
        return reservDays;
      case CUSTOM_LVL:
        return hours / 24;
    }
  }

  export {
    reservDays,
    reservLevel as result
  }

</script>

<div class="row {$$props.class ? $$props.class : ''}">
  <div class="col-12 col-lg-4 mb-3">
    <h5 class="sectionTitle d-block mb-1" >Уровень резервирования</h5>
  </div>
  <div class="col">
    <select bind:value={level} >
      <option value={FULL_LVL}>Полный резерв, без отключений</option>
      <option value={PART_LVL}>Полный резерв, отключение допустимо</option>
      <option value={CUSTOM_LVL}>Резерв на заданный промежуток времени</option>
    </select>
    <div class="row">
      {#if level === CUSTOM_LVL}
        <InputNumber
          class="col-12 col-sm-6 col-md-4 mt-3"
          label="Кол-во часов резерва"
          bind:value={hours}
          min="0"
          sign="ч"
        />
      {/if}
    </div>
  </div>
</div>