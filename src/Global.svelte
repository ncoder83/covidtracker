<script>
  import Card from "./components/Card.svelte";
  import { onMount } from "svelte";

  let as_of;
  let new_confirmed;
  let total_confirmed;

  let new_deaths;
  let total_deaths;

  let new_recovered;
  let total_recovered;

  onMount(() => {
    var requestOptions = {
      method: "GET",
      redirect: "follow"
    };
    fetch("https://api.covid19api.com/summary", requestOptions)
      .then(response => response.json())
      .then(data => {
        as_of = data.Date;
        let global = data.Global;

        new_confirmed = global.NewConfirmed;
        total_confirmed = global.TotalConfirmed;

        new_deaths = global.NewDeaths;
        total_deaths = global.TotalDeaths;

        new_recovered = global.NewRecovered;
        total_recovered = global.TotalRecovered;
      })
      .catch(error => console.log("error", error));
  });
</script>

<h3 class="text-secondary">Global({as_of})</h3>

<div class="row">
  <div class="col">
    <Card
      title="New confirmed"
      text={new_confirmed || 'N/A'}
      textstyle="text-warning" />
  </div>
  <div class="col">
    <Card
      title="Total confirmed"
      text={total_confirmed || 'N/A'}
      textstyle="text-warning" />
  </div>
</div>

<div class="row">
  <div class="col">
    <Card
      title="New recovered"
      text={new_recovered || 'N/A'}
      textstyle="text-success" />
  </div>
  <div class="col">
    <Card
      title="Total recovered"
      text={total_recovered || 'N/A'}
      textstyle="text-success" />
  </div>
</div>

<div class="row">
  <div class="col">
    <Card
      title="New deaths"
      text={new_deaths || 'N/A'}
      textstyle="text-danger" />
  </div>
  <div class="col">
    <Card
      title="Total deaths"
      text={total_deaths || 'N/A'}
      textstyle="text-danger" />
  </div>
</div>
