<script>
  export let powerСonsum;
  export let hoursDay;
  export let sunDays;
  export let reservLvl;
  export let powerVolt;

  $: batteryPowerA = Number((powerСonsum * reservLvl / powerVolt).toFixed(2));
  $: batteryPowerW = Number((powerСonsum * reservLvl).toFixed(2));
  $: dayGen100 = Number(((100 * 0.45 * 2) + (100 * 0.77 * (hoursDay - 2))).toFixed(2));
  $: dayGen100Load = Number((dayGen100 - powerСonsum).toFixed(2));
  $: dayGen250 = Number(((100 * 0.45 * 2) + (250 * 0.77 * (hoursDay - 2))).toFixed(2));
  $: dayGen250Load = Number((dayGen250 - powerСonsum).toFixed(2));
</script>

<div class="row {$$props.class ? $$props.class : ''}">
  <div class="col-12"></div>
  <h5 class="sectionTitle col-12 col-lg-4 mt-0 mb-3">Результат</h5>
  <div class="col">
    <div class="result-list row">
      <p class="col-12 mb-2 mt-0">
        <span class="d-block d-xs-inline mb-1 mb-xs-0 mr-xs-2">Требуемая емкость АКБ:</span>
        <span class="result-value">{batteryPowerA}</span> А
      </p>
      <p class="col-12 mb-2 mt-0">
        <span class="d-block d-xs-inline mb-1 mb-xs-0 mr-xs-2">Требуемая емкость АКБ:</span>
        <span class="result-value">{batteryPowerW}</span> Вт
      </p>
      <p class="col-12 mb-2 mt-0">
        <span class="d-block d-xs-inline mb-1 mb-xs-0 mr-xs-2">Суточное потребление:</span>
        <span class="result-value">{powerСonsum}</span> Вт
      </p>
      <p class="col-12 mb-3 mb-sm-4 mt-0">
        <span class="d-block d-xs-inline mb-1 mb-xs-0 mr-xs-2">
          Заданное кол-во солнечных дней в худший месяц:
        </span>
        <span class="result-value">{sunDays}</span> дн.
      </p>
      <p class="col-12 col-sm-6 mb-3 mb-sm-4 mt-0">
        Расчетная суточная генерация 100&nbsp;Вт панели без нагрузки:
        <span class="d-block mt-1">
          <span class="result-value">{dayGen100}</span> Вт
        </span>
      </p>
      <p class="col-12 col-sm-6 mb-3 mb-sm-4 mt-0">
        Расчетная суточная генерация 100&nbsp;Вт панели с нагрузкой:
        <span class="d-block mt-1">
          <span class="result-value">{dayGen100Load}</span> Вт
        </span>
      </p>
      <p class="col-12 col-sm-6 mb-3 mb-sm-4 mt-0">
        Расчетная суточная генерация 250&nbsp;Вт панели без нагрузки:
        <span class="d-block mt-1">
          <span class="result-value">{dayGen250}</span> Вт
        </span>
      </p>
      <p class="col-12 col-sm-6 mb-3 mb-sm-4 mt-0">
        Расчетная суточная генерация 250&nbsp;Вт панели с нагрузкой:
        <span class="d-block mt-1">
          <span class="result-value">{dayGen250Load}</span> Вт
        </span>
      </p>
    </div>
  </div>
</div>
