<script>
  import LoadSetup from "./LoadSetup.svelte";         // Параметры нагрузки
  import SunDays from "./SunDays.svelte";             // Кол-во солнечных дней
  import ReservLevel from "./ReservLevel.svelte";     // Уровень резервирования
  import PowerVoltage from "./PowerVoltage.svelte";   // Напряжение питания нагрузки
  import CalcResult from "./CalcResult.svelte";       // Итоги

  let powerСonsum;
  let hoursDay;
  let sunDays;
	let reservDays;
  let reservLvl;
  let powerVolt;
</script>

<form autocomplete="off">
  <p class="warning_info mb-5">
    Данные расчеты являются ориентировочными и не гарантируют полного соответствия
    с показателями работы системы в реальных условиях.
  </p>
  <LoadSetup bind:result={powerСonsum} bind:hoursDay={hoursDay} />
  <SunDays class="mt-4 mt-md-5" bind:result={reservDays} bind:sunDays={sunDays} />
  <ReservLevel class="mt-4 mt-md-5" bind:result={reservLvl} reservDays={reservDays} />
  <PowerVoltage class="mt-4 mt-md-5" bind:result={powerVolt} />
  <CalcResult
    class="mt-4 mt-md-5"
    powerСonsum={powerСonsum}
    hoursDay={hoursDay}
    sunDays={sunDays}
    reservLvl={reservLvl}
    powerVolt={powerVolt}
  />
</form>

<style src="./app-style.scss" global></style>