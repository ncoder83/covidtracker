<script>
  import { onMount } from "svelte";
  export var bookmark;

  let countries = [];
  let as_of;
  let country_filter = bookmark || "";

  $: filtered_result = country_filter
    ? countries.filter(c => {
        return c.Country.toLowerCase().startsWith(country_filter.toLowerCase());
      })
    : countries;

  onMount(() => {
    var requestOptions = {
      method: "GET",
      redirect: "follow"
    };

    fetch("https://api.covid19api.com/summary", requestOptions)
      .then(response => response.json())
      .then(data => {
        as_of = data.Date;
        countries = data.Countries;
      })
      .catch(error => console.log("error", error));
  });
</script>

<h3>Countries ({as_of})</h3>

<input
  type="text"
  class="form-control"
  placeholder="Filter countries"
  bind:value={country_filter} />

<div class="overflow-auto" style="height:300px;">

  {#each filtered_result as country}
    <ul class="list-unstyled">
      <li>
        <b>Name: {country.Country}</b>
        <ul>
          <li>
            New confirmed:
            <span class="text-warning">{country.NewConfirmed}</span>
          </li>
          <li>
            Total Confirmed:
            <span class="text-warning">{country.TotalConfirmed}</span>
          </li>
          <li>
            New Recovered:
            <span class="text-success">{country.NewRecovered}</span>
          </li>
          <li>
            Total Recovered:
            <span class="text-success">{country.TotalRecovered}</span>
          </li>
          <li>
            New Deaths:
            <span class="text-danger">{country.NewDeaths}</span>
          </li>
          <li>
            Total Deaths:
            <span class="text-danger">{country.TotalDeaths}</span>
          </li>
        </ul>
      </li>
    </ul>
  {/each}

</div>
