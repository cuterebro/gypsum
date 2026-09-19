<script>
  let state = {
    volume: 300,
    density: 2,
    gypsum: 100,
    water: 28,
    plasticizer: 2,
    pigment: 0,
    reserve: 10
  }

  $: weight = state.volume * state.density * (1 + state.reserve/100)
  $: fractions = state.gypsum + state.water + state.plasticizer + state.pigment
  $: gypsum = weight * state.gypsum / fractions 
  $: water = weight * state.water / fractions 
  $: plasticizer = weight * state.plasticizer / fractions 
  $: pigment = weight * state.pigment / fractions 

</script>

<div id='calculator'>
  <div id='inputs'>
    <h3>Исходные данные</h3>
    <div class='input'>
      <label>Объём формы, мл:</label>
      <input name=volume min=0 type=number bind:value={state.volume} />  
    </div>

    <div class='input'>
      <label>Плотность смеси, г/мл:</label>
      <input name=volume type=number min=0.1 step=0.1 bind:value={state.density} />
    </div>

    <div class='input'>
      <label>Гипс, массовые доли:</label>
      <input name=volume type=number min=0 bind:value={state.gypsum} />
    </div>

    <div class='input'>
      <label>Вода, массовые доли:</label>
      <input name=volume type=number min=0 bind:value={state.water} />
    </div>

    <div class='input'>
      <label>Пластификатор, массовые доли:</label>
      <input name=volume type=number min=0 bind:value={state.plasticizer} />
    </div>

    <div class='input'>
      <label>Пигмент, массовые доли:</label>
      <input name=volume type=number min=0 bind:value={state.pigment} />
    </div>

    <div class='input'>
      <label>Запас, %:</label>
      <input name=volume type=number min=0 bind:value={state.reserve} />
    </div>  
  </div>

  <div id='recipe'>
    <h3>Рецепт</h3>
    <div class='output'><span>Вес отливки:</span> <span class='value'>{Math.round(weight)}</span> г</div>
    <div class='output'><span>Гипс:</span> <span class='value'>{Math.round(gypsum)}</span> г</div>
    <div class='output'><span>Вода:</span> <span class='value'>{Math.round(water)}</span> г</div>
    <div class='output'><span>Пластификатор:</span> <span class='value'>{Math.round(plasticizer)}</span> г</div>
    <div class='output'><span>Пигмент:</span> <span class='value'>{Math.round(pigment)}</span> г</div>
  </div>
</div>