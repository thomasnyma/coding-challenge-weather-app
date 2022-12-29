<script lang="ts">
  import { onMount } from "svelte";
  const endpoint = "https://api.api-ninjas.com/v1/inflation?country=";
//   let country = 'denmark';

    interface InflationInfo {
        "country": string,
        "type": string,
        "period": string,
        "monthly_rate_pct": number,
        "yearly_rate_pct": number
    }

  let inflationInfo: InflationInfo | undefined;

  onMount(async function () {
    getInflationInfo('denmark')
  });

  async function getInflationInfo(country: string) {
    await fetch(endpoint + country, {
		method: 'GET',
		headers: {
            'X-Api-Key': import.meta.env.VITE_WEATHERAPI
		},
    })
    	.then(response => response.json())
		.then(response => inflationInfo = response[0])
		.catch(err => console.error(err));    
  }
  
  function onSubmit(e: any) {
    const formData = new FormData(e.target);

    const data = {};
    for (let field of formData) {
      const [key, value] = field;
      data[key] = value;
    }
    getInflationInfo(data['country'])
  }

</script>

<div>
    <form on:submit|preventDefault={onSubmit}>
        <div>
            <label for="name">Country</label>
            <input
              type="text"
              id="country"
              name="country"
              value=""
              class="p-2 rounded-lg bg-slate-100 dark:bg-slate-700"
            />
        </div>
        <button type="submit" class="p-2 rounded-lg transition hover:bg-slate-100 dark:hover:bg-slate-700">Submit</button>
    </form>

    <br>

    {#if inflationInfo}
        <h2>The current inflation rate for {inflationInfo.country} in {inflationInfo.period} is at {inflationInfo.monthly_rate_pct}%</h2>
        <span>The yearly inflation is {inflationInfo.yearly_rate_pct}%</span>
    {:else}
        <span>No data yet...</span>
    {/if}
</div>