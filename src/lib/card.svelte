<div class="card">
  <div><slot name="title" /></div>
  <div class="subtitle">
    <slot name="subtitle" />
  </div>
  <div class="value">
    <slot name="value" />
  </div>
</div>

<style>
  .card {
    border-radius: var(--radii);
    border: 1px solid #999;
    padding: 2rem;
    display: flex;
    flex-direction: column;
    font-weight: 600;
  }

  .subtitle {
    color: #999;
    font-size: 0.95rem;
    font-weight: 500;
  }

  .value {
    font-size: 4rem;
    font-weight: 600;
  }
</style>
