<script lang="ts">
    export let text: string;
</script>

<div class="section-header">
    <hr />
    <h1 class="gradient-text">{text}</h1>
    <hr />
</div>

<style>
    .section-header {
      display: flex;
      align-items: center;
      gap: 1rem;
    }

    .section-header hr {
      width: 3.5rem;
      color: var(--gray-400)
    }

    .section-header h1 {
      font-family: LaurentianStd-It;
      font-size: 3.15rem;
    }
</style>