<script>
  /**
   * Main App Component
   * 
   * This is the root component of our Svelte 5 calculator application.
   * It imports and displays the Calculator component.
   */
  import Calculator from './lib/Calculator.svelte'
</script>

<main>
  <!-- App title -->
  <h1>Simple Calculator</h1>
  
  <!-- Brief description for beginners -->
  <p class="subtitle">Built with Svelte 5</p>
  
  <!-- Calculator component -->
  <div class="calculator-container">
    <Calculator />
  </div>
  
  <!-- Footer information -->
  <p class="footer">
    A beginner-friendly calculator demonstrating Svelte 5 features
  </p>
</main>

<style>
  main {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    padding: 2rem;
  }

  h1 {
    font-size: 2.5em;
    margin-bottom: 0.5rem;
    color: #ffffff;
  }

  .subtitle {
    font-size: 1.2em;
    color: #888;
    margin-bottom: 2rem;
  }

  .calculator-container {
    margin-bottom: 2rem;
  }

  .footer {
    color: #666;
    font-size: 0.9em;
    text-align: center;
    max-width: 400px;
  }

  /* Light mode styles */
  @media (prefers-color-scheme: light) {
    h1 {
      color: #213547;
    }
  }
</style>
