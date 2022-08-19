<script>
  import Card from "./lib/card.svelte";

  let ticket = 400;
  let leads = 20;
  let profit_margin = 70;
  let close_rate = 50;

  $: total_new_leads = leads * close_rate * 0.01;
  $: actual_lead_value = (total_new_leads * ticket) / leads;
  $: lead_net_margin = actual_lead_value * profit_margin * 0.01;

  function round(value, places = 0) {
    return value.toFixed(places);
  }
</script>

<main>
  <h1>Calculadora de Valor de Clientes</h1>

  <div>
    <label for="ticket">
      Valor médio p/cliente:
      <input
        name="ticket"
        type="number"
        placeholder="100"
        bind:value={ticket}
      />
    </label>
  </div>

  <div>
    <label for="leads">
      Quantidade de clientes p/mês:
      <input name="leads" type="number" placeholder="30" bind:value={leads} />
    </label>
  </div>

  <div>
    <label for="profit-margin">
      Margem de lucro média (%):
      <input
        name="profit-margin"
        type="range"
        min="0"
        step="5"
        max="100"
        bind:value={profit_margin}
      />
    </label>
    {profit_margin}
  </div>

  <div>
    <label for="close-rate">
      Taxa de conversão média (%):
      <input
        name="close-rate"
        type="range"
        min="0"
        step="5"
        max="100"
        bind:value={close_rate}
      />
      {close_rate}
    </label>
  </div>

  <div class="grid">
    <Card>
      <span slot="title">Lucro Médio Pós Despesas</span>
      <span slot="subtitle">Excluindo Marketing</span>
      <span slot="value">{round(ticket * profit_margin * 0.01)} €</span>
    </Card>

    <Card>
      <span slot="title">Total de Novos Clientes</span>
      <span slot="subtitle">Para a Empresa</span>
      <span slot="value">{round(total_new_leads)}</span>
    </Card>

    <Card>
      <span slot="title">Valor Real de Cliente</span>
      <span slot="subtitle">Para a Empresa</span>
      <span slot="value">{round(actual_lead_value)} €</span>
    </Card>

    <Card>
      <span slot="title">Margem Líquida p/ Cliente</span>
      <span slot="subtitle">Valor Real * Margem de Lucro</span>
      <span slot="value">{round(lead_net_margin)} €</span>
    </Card>

    <Card>
      <span slot="title">Faturação Mensal</span>
      <span slot="subtitle">Para a Empresa</span>
      <span slot="value" class="green">{round(actual_lead_value * leads)} €</span>
    </Card>

    <Card>
      <span slot="title">Lucro Mensal</span>
      <span slot="subtitle">Excluindo Marketing</span>
      <span slot="value" class="green">{round(lead_net_margin * leads)} €</span>
    </Card>
  </div>

  <hr />

  <Card>
    <span slot="title">Valor a cobrar</span>
    <span slot="subtitle">Por cliente enviado</span>
    <span slot="value"
      >{round(lead_net_margin * 0.25)} - {round(lead_net_margin * 0.4)} €</span
    >
  </Card>

  <Card>
    <span slot="title">Valor a cobrar</span>
    <span slot="subtitle">Total Mensal</span>
    <span slot="value"
      >{round(lead_net_margin * leads * 0.25)} - {round(
        lead_net_margin * leads * 0.4
      )} €</span
    >
  </Card>
</main>

<style>
  .grid {
    display: grid;
    grid-template-columns: 1fr;
    gap: 1rem;
    margin-top: 2.4rem;
  }

  .green {
    color: rgb(15, 170, 15);
  }

  @media (min-width: 580px) {
    .grid {
      grid-template-columns: 1fr 1fr;
    }
  }

  @media (min-width: 720px) {
    .grid {
      grid-template-columns: 1fr 1fr 1fr;
    }
  }
</style>
