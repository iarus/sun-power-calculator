<script>
  import InputNumber from "./InputNumber.svelte";

  const COMMON_TYPE = "common";
  const SPLIT_TYPE = "split";
  let type = COMMON_TYPE;
  let typeCheckbox = false;
  let power = { day: 2.1, night: 0.3 };
  let hours = { day: 14, night: 10 };
  let powerInput = 0;
  let hoursDay;

  $: hoursDay = hours.day;
  $: hours.night = 24 - hours.day;
  $: powerInput = Number(getDayPowerInput(type, power, hours).toFixed(2));
  $: type = typeCheckbox ? SPLIT_TYPE : COMMON_TYPE;

  function getDayPowerInput() {
    switch (type) {
      case COMMON_TYPE:
        return power.day * 24;
      case SPLIT_TYPE:
        return power.day * hours.day + power.night * hours.night;
    }
  }

  export {
    powerInput as result,
    hoursDay,
  }
</script>

<div class="row">
  <h5 class="sectionTitle col-12 col-lg-4 mb-3">Нагрузка, потребление</h5>
  <div class="col">
    <div class="row align-items-end">
      {#if type == COMMON_TYPE}
        <InputNumber
          class="col-12 col-sm-6 mb-3"
          label="Потребление нагрузки, в час"
          bind:value={power.day}
          step="0.1"
          min="0"
          sign="Вт/ч"
        />
      {:else}
        <InputNumber
          class="col-12 col-sm-6 mb-3"
          label="Потребление нагрузки днем, в час"
          bind:value={power.day}
          step="0.1"
          min="0"
          sign="Вт/ч"
        />
        <InputNumber
          class="col-12 col-sm-6 mb-3"
          label="Потребление нагрузки ночью, в час"
          bind:value={power.night}
          step="0.1"
          min="0"
          sign="Вт/ч"
        />
      {/if}
    </div>

    <label class="d-flex align-items-center">
      <input class="mr-2" type="checkbox" bind:checked={typeCheckbox}> Раздельное потребление
    </label>
  </div>
</div>

<div class="row mt-4 mt-md-5">
  <div class="col-12 col-lg-4 mb-3 mb-lg-0">
    <h5 class="sectionTitle d-block mb-1" >Количество часов</h5>
    <p class="comment">
      Кол-во часов дня и ночи можно узнать, например, на сайте
      <a href="https://voshod-solnca.ru/countries/%D1%80%D0%BE%D1%81%D1%81%D0%B8%D1%8F"
        target="_blank" rel="noopener noreferrer">https://voshod-solnca.ru</a>
    </p>
  </div>
  <div class="col">
    <div class="d-flex justify-content-between mb-2">
      <span>☀ День <b>{hours.day} ч</b></span>
      <span>☽ Ночь <b>{hours.night} ч</b></span>
    </div>
    <input class="w-100" type="range" min="0" max="24" bind:value={hours.day}>
  </div>
</div>