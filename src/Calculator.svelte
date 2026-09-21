<script>
  const key = 'gypsum_state';
  const default_state = {
    volume: 300,
    density: 2,
    gypsum: 100,
    water: 28,
    plasticizer: 2,
    pigment: 0,
    reserve: 10
  }

  let stored = (typeof window !== 'undefined' && localStorage.getItem(key));
  let state = $state(stored ? JSON.parse(stored) : default_state)

  $effect(() => {
    localStorage.setItem(key, JSON.stringify($state.snapshot(state)));
  });

  let weight = $derived(state.volume * state.density * (1 + state.reserve/100))
  let fractions = $derived(state.gypsum + state.water + state.plasticizer + state.pigment)
  let gypsum = $derived(weight * state.gypsum / fractions)
  let water = $derived(weight * state.water / fractions)
  let plasticizer = $derived(weight * state.plasticizer / fractions)
  let pigment = $derived(weight * state.pigment / fractions)

</script>

<div id='calculator'>
  <div id='inputs'>
    <h3>Исходные данные</h3>
    <div class='input'>
      <label for=volume>Объём формы, мл:</label>
      <input name=volume min=0 type=number bind:value={state.volume} />  
    </div>

    <div class='input'>
      <label for=density>Плотность смеси, г/мл:</label>
      <input name=density type=number min=0.1 step=0.1 bind:value={state.density} />
    </div>

    <div class='input'>
      <label for=gypsum>Гипс, массовые доли:</label>
      <input name=gypsum type=number min=0 bind:value={state.gypsum} />
    </div>

    <div class='input'>
      <label for=water>Вода, массовые доли:</label>
      <input name=water type=number min=0 bind:value={state.water} />
    </div>

    <div class='input'>
      <label for=plasticizer>Пластификатор, массовые доли:</label>
      <input name=plasticizer type=number min=0 bind:value={state.plasticizer} />
    </div>

    <div class='input'>
      <label for=pigment>Пигмент, массовые доли:</label>
      <input name=pigment type=number min=0 bind:value={state.pigment} />
    </div>

    <div class='input'>
      <label for=reserve>Запас, %:</label>
      <input name=reserve type=number min=0 bind:value={state.reserve} />
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