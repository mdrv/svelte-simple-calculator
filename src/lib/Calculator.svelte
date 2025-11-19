<script>
  /**
   * Calculator Component
   * A simple calculator built with Svelte 5
   * 
   * This component demonstrates:
   * - Svelte 5's $state rune for reactive state management
   * - Event handling with onclick
   * - Dynamic class binding
   * - String manipulation and number operations
   */

  // State variables using Svelte 5's $state rune
  // $state makes variables reactive - when they change, the UI updates automatically
  let display = $state('0'); // The current display value
  let previousValue = $state(null); // The previous number entered
  let operator = $state(null); // The current operation (+, -, *, /)
  let waitingForNewValue = $state(false); // Flag to know if we should start a new number

  /**
   * Handles number button clicks
   * @param {string} num - The number that was clicked (0-9)
   */
  function appendNumber(num) {
    // If we're waiting for a new value (after an operator was pressed)
    // or if display is currently '0', replace it with the new number
    if (waitingForNewValue || display === '0') {
      display = num;
      waitingForNewValue = false;
    } else {
      // Otherwise, append the number to the existing display
      display = display + num;
    }
  }

  /**
   * Handles decimal point button click
   */
  function appendDecimal() {
    // If we're waiting for a new value, start with "0."
    if (waitingForNewValue) {
      display = '0.';
      waitingForNewValue = false;
    } else if (!display.includes('.')) {
      // Only add decimal if there isn't one already
      display = display + '.';
    }
  }

  /**
   * Handles operator button clicks (+, -, *, /)
   * @param {string} op - The operator that was clicked
   */
  function setOperator(op) {
    // If there's a previous calculation waiting, calculate it first
    if (previousValue !== null && operator !== null && !waitingForNewValue) {
      calculate();
    }
    
    // Store the current display value and operator
    previousValue = parseFloat(display);
    operator = op;
    waitingForNewValue = true;
  }

  /**
   * Performs the calculation based on the stored operator
   */
  function calculate() {
    // If we don't have the necessary values, do nothing
    if (previousValue === null || operator === null) {
      return;
    }

    const current = parseFloat(display);
    let result;

    // Perform the calculation based on the operator
    switch (operator) {
      case '+':
        result = previousValue + current;
        break;
      case '-':
        result = previousValue - current;
        break;
      case '*':
        result = previousValue * current;
        break;
      case '/':
        // Handle division by zero
        result = current === 0 ? 'Error' : previousValue / current;
        break;
      default:
        return;
    }

    // Update the display with the result
    // If result is a number, round to avoid floating point precision issues
    display = typeof result === 'number' ? String(Math.round(result * 100000000) / 100000000) : result;
    
    // Reset the calculator state
    previousValue = null;
    operator = null;
    waitingForNewValue = true;
  }

  /**
   * Clears the calculator (AC = All Clear)
   */
  function clear() {
    display = '0';
    previousValue = null;
    operator = null;
    waitingForNewValue = false;
  }

  /**
   * Toggles the sign of the current number (positive/negative)
   */
  function toggleSign() {
    if (display !== '0') {
      display = display.startsWith('-') ? display.slice(1) : '-' + display;
    }
  }

  /**
   * Converts the current number to a percentage (divides by 100)
   */
  function percentage() {
    const num = parseFloat(display);
    display = String(num / 100);
  }
</script>

<!-- Calculator UI -->
<div class="calculator">
  <!-- Display screen showing current value -->
  <div class="display">{display}</div>
  
  <!-- Calculator buttons grid -->
  <div class="buttons">
    <!-- Row 1: Clear, +/-, %, ÷ -->
    <button class="btn function" onclick={clear}>AC</button>
    <button class="btn function" onclick={toggleSign}>+/-</button>
    <button class="btn function" onclick={percentage}>%</button>
    <button class="btn operator" onclick={() => setOperator('/')}>÷</button>
    
    <!-- Row 2: 7, 8, 9, × -->
    <button class="btn" onclick={() => appendNumber('7')}>7</button>
    <button class="btn" onclick={() => appendNumber('8')}>8</button>
    <button class="btn" onclick={() => appendNumber('9')}>9</button>
    <button class="btn operator" onclick={() => setOperator('*')}>×</button>
    
    <!-- Row 3: 4, 5, 6, - -->
    <button class="btn" onclick={() => appendNumber('4')}>4</button>
    <button class="btn" onclick={() => appendNumber('5')}>5</button>
    <button class="btn" onclick={() => appendNumber('6')}>6</button>
    <button class="btn operator" onclick={() => setOperator('-')}>-</button>
    
    <!-- Row 4: 1, 2, 3, + -->
    <button class="btn" onclick={() => appendNumber('1')}>1</button>
    <button class="btn" onclick={() => appendNumber('2')}>2</button>
    <button class="btn" onclick={() => appendNumber('3')}>3</button>
    <button class="btn operator" onclick={() => setOperator('+')}>+</button>
    
    <!-- Row 5: 0 (spans 2 columns), ., = -->
    <button class="btn zero" onclick={() => appendNumber('0')}>0</button>
    <button class="btn" onclick={appendDecimal}>.</button>
    <button class="btn operator" onclick={calculate}>=</button>
  </div>
</div>

<style>
  /* Main calculator container */
  .calculator {
    background: #1a1a1a;
    border-radius: 20px;
    padding: 20px;
    width: 320px;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
  }

  /* Display screen */
  .display {
    background: #2d2d2d;
    color: #ffffff;
    font-size: 48px;
    text-align: right;
    padding: 20px;
    border-radius: 10px;
    margin-bottom: 20px;
    min-height: 60px;
    display: flex;
    align-items: center;
    justify-content: flex-end;
    overflow: hidden;
    word-break: break-all;
  }

  /* Buttons grid container */
  .buttons {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 12px;
  }

  /* Base button styles */
  .btn {
    background: #505050;
    border: none;
    border-radius: 50%;
    color: #ffffff;
    font-size: 24px;
    padding: 0;
    height: 65px;
    width: 65px;
    cursor: pointer;
    transition: all 0.2s;
    font-weight: 400;
  }

  /* Button hover effect */
  .btn:hover {
    background: #6a6a6a;
    transform: scale(1.05);
  }

  /* Button active (pressed) effect */
  .btn:active {
    transform: scale(0.95);
  }

  /* Function buttons (AC, +/-, %) */
  .btn.function {
    background: #a5a5a5;
    color: #000000;
  }

  .btn.function:hover {
    background: #c0c0c0;
  }

  /* Operator buttons (+, -, ×, ÷, =) */
  .btn.operator {
    background: #ff9500;
  }

  .btn.operator:hover {
    background: #ffb143;
  }

  /* Zero button spans 2 columns */
  .btn.zero {
    grid-column: span 2;
    border-radius: 35px;
    width: 142px;
  }

  /* Responsive design for smaller screens */
  @media (max-width: 400px) {
    .calculator {
      width: 280px;
    }

    .btn {
      height: 55px;
      width: 55px;
      font-size: 20px;
    }

    .btn.zero {
      width: 122px;
    }

    .display {
      font-size: 36px;
      padding: 15px;
    }
  }
</style>
