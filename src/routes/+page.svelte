<script lang="ts">
  let shutterSpeedUnits = ['μs', 'ms', 's']
  let unitsValues: {[key: string]: number} = {
    'μs': 1,
    'ms': 1000,
    's': 1000000
  }
  
  let customDimensions = false;
  let inputWidth = 640;
  let inputHeight = 480;
  $: width = customDimensions ? inputWidth : 0;
  $: height = customDimensions ? inputHeight : 0;
  let gainIso = 100;
  let inputShutterSpeed = 0;
  let shutterSpeedUnit = 'μs';
  $: shutterSpeed = inputShutterSpeed * unitsValues[shutterSpeedUnit];
  let showImageOptions = false;
  let inputBrightness = 0.0;
  let inputContrast = 1.0;
  let inputSaturation = 1.0;
  let inputSharpness = 1.0;
  $: brightness = showImageOptions ? inputBrightness : 0.0;
  $: contrast = showImageOptions ? inputContrast : 1.0;
  $: saturation = showImageOptions ? inputSaturation : 1.0;
  $: sharpness = showImageOptions ? inputSharpness : 1.0;
  
  function resetToDefault() {
    customDimensions = false;
    inputWidth = 640;
    inputHeight = 480;
    gainIso = 100;
    brightness = 0.0;
    contrast = 1.0;
    saturation = 1.0;
    sharpness = 1.0;
    showImageOptions = false;
  }
</script>

<div class="flex flex-col min-h-screen items-center justify-center">
  <h1 class="text-5xl mb-4 bg-gradient-to-r from-purple-500 to-sky-600 text-transparent bg-clip-text">Alderaan</h1>

  <div class="flex-1 flex flex-col items-center text-2xl gap-5 w-96">
    <button class="bg-blue-500 hover:bg-sky-600 active:bg-sky-700 transition px-4 py-2 rounded" on:click={resetToDefault}>Reset to Default</button>

    <div class="grid grid-cols-2 items-baseline">
      <span class="text-2xl flex flex-row items-center justify-center col-span-2">
        <input type="checkbox" bind:checked={customDimensions} class="mr-2" /> Custom Dimensions
      </span>
      
      {#if customDimensions}
        <span>Width</span>
        <input type="number" bind:value={inputWidth} class="h-10 mb-2" />

        <span>Height</span>
        <input type="number" bind:value={inputHeight} class="h-10 mb-2" />
      {/if}
    </div>

    <div class="grid grid-cols-2 items-baseline">
      <span>ISO</span>
      <input type="number" bind:value={gainIso} class="h-10 mb-2" />
    </div>

    <div class="grid grid-cols-2 items-baseline">
      <span>Shutter Speed</span>
      <input type="number" bind:value={inputShutterSpeed} class="h-10 mb-2" />

      <span>Unit</span>
      <select bind:value={shutterSpeedUnit} class="h-10 mb-2">
        {#each shutterSpeedUnits as unit}
          <option value={unit}>{unit}</option>
        {/each}
      </select>
    </div>

    <div class="grid grid-cols-2 items-baseline">
      <span class="text-2xl flex flex-row items-center justify-center col-span-2">
        <input type="checkbox" bind:checked={showImageOptions} class="mr-2" /> Image Options
      </span>
      
      {#if showImageOptions}
        <span>Brightness</span>
        <input type="number" bind:value={inputBrightness} class="h-10 mb-2" min="0" max="1" step="any" />

        <span>Contrast</span>
        <input type="number" bind:value={inputContrast} class="h-10 mb-2" min="0" max="1" step="any" />

        <span>Saturation</span>
        <input type="number" bind:value={inputSaturation} class="h-10 mb-2" min="0" max="1" step="any" />

        <span>Sharpness</span>
        <input type="number" bind:value={inputSharpness} class="h-10 mb-2" min="0" max="1" step="any" />
      {/if}
    </div>
  </div>
</div>
