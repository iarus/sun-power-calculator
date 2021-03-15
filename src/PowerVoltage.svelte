<script>
  let voltage;

  let voltList = [
    { value: 12, text: "12 В" },
    { value: 24, text: "24 В" },
    { value: 220, text: "220 В" }
  ]

  export {
    voltage as result
  }
</script>

<div class="row {$$props.class ? $$props.class : ''}">
  <div class="col-12 col-lg-4 mb-3">
    <h5 class="sectionTitle d-block mb-1" >Напряжение питания нагрузки</h5>
  </div>
  <div class="col">
    <select bind:value={voltage}>
      {#each voltList as item}
        <option value={item.value}>{item.text}</option>
      {/each}
    </select>
    {#if voltage == 220}
      <p class="comment mt-3">
        Для реализации питания сетей 220В в систему потребуется включить инвертор.
        Выбор инвертора осуществляется самостоятельно по параметрам запитываемой сети.
      </p>
    {/if}
  </div>
</div>