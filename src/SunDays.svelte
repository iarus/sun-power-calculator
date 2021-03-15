<script>
  import InputNumber from "./InputNumber.svelte";

  let days = 1;
  let reservDays = 1;
  $: reservDays = Number((31 / days).toFixed(2));

  export {
    reservDays as result,
    days as sunDays
  }
</script>

<div class="row {$$props.class ? $$props.class : ''}">
  <div class="col-12 col-lg-4 mb-3 mb-lg-0">
    <h5 class="sectionTitle d-block mb-1" >Количество солнечных дней</h5>
    <p class="comment">
      Кол-во солнечных дней может быть получено на сайте
      <a href="http://weatherarchive.ru/" target="_blank" rel="noopener noreferrer">http://weatherarchive.ru/</a>
    </p>
  </div>
  <div class="col">
    <div class="row">
      <InputNumber
        class="d-block col-12 col-sm-4 col-md-4 mb-2"
        bind:value={days}
        step="1"
        min="1"
        max="31"
        sign="дн."
      />
    </div>
    <p>
      Кол-во солнечных дней в худший месяц в периоде эксплуатации
    </p>
  </div>
</div>