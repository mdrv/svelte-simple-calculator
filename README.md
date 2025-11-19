# Svelte Simple Calculator

A simple, beginner-friendly calculator web application built with **Svelte 5** and **Vite**.

![Calculator Demo](https://img.shields.io/badge/Svelte-5-FF3E00?style=flat&logo=svelte&logoColor=white)
![Vite](https://img.shields.io/badge/Vite-7-646CFF?style=flat&logo=vite&logoColor=white)

## 🎯 Features

- ✨ Clean and modern UI design
- ➕ Basic arithmetic operations (addition, subtraction, multiplication, division)
- 🔢 Decimal point support
- 🔄 Sign toggle (+/-)
- 📊 Percentage calculations
- 🧹 Clear/Reset functionality
- 📱 Responsive design for mobile devices
- 💡 Well-commented code for learning purposes

## 🚀 Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) (version 16 or higher)
- npm (comes with Node.js)

### Installation

1. Clone this repository:
```bash
git clone https://github.com/mdrv/svelte-simple-calculator.git
cd svelte-simple-calculator
```

2. Install dependencies:
```bash
npm install
```

3. Start the development server:
```bash
npm run dev
```

4. Open your browser and navigate to `http://localhost:5173` (or the URL shown in your terminal)

## 🏗️ Building for Production

To create a production build:

```bash
npm run build
```

To preview the production build:

```bash
npm run preview
```

## 📚 Learning Resources

This project is designed to help beginners understand:

### Svelte 5 Features Used

1. **`$state` rune** - Svelte 5's new way to create reactive state
   ```javascript
   let display = $state('0'); // Reactive variable
   ```

2. **Event Handling** - Using `onclick` to handle user interactions
   ```svelte
   <button onclick={() => appendNumber('7')}>7</button>
   ```

3. **Component Structure** - Organizing code into reusable components
   - `App.svelte` - Main application component
   - `Calculator.svelte` - Calculator logic and UI

4. **Styling** - Component-scoped CSS styles

### Project Structure

```
svelte-simple-calculator/
├── src/
│   ├── lib/
│   │   └── Calculator.svelte    # Main calculator component
│   ├── App.svelte               # Root component
│   ├── main.js                  # Application entry point
│   └── app.css                  # Global styles
├── public/                      # Static assets
├── index.html                   # HTML template
├── package.json                 # Project dependencies
└── vite.config.js              # Vite configuration
```

### How the Calculator Works

1. **State Management**: The calculator uses Svelte 5's `$state` rune to manage reactive variables:
   - `display` - Current number shown on screen
   - `previousValue` - Stores the first number in an operation
   - `operator` - Stores the selected operation (+, -, ×, ÷)
   - `waitingForNewValue` - Flag to determine if we should start a new number

2. **Number Input**: When you click a number button, it either:
   - Replaces the display (if starting fresh)
   - Appends to the current display (if continuing)

3. **Operations**: When you click an operator:
   - Stores the current number
   - Remembers which operation you selected
   - Waits for the next number

4. **Calculation**: When you press `=`:
   - Takes the stored number and current number
   - Performs the selected operation
   - Shows the result

## 🎨 Customization

You can easily customize the calculator's appearance by modifying the styles in `src/lib/Calculator.svelte`:

- Change colors: Modify the `background`, `color` properties
- Adjust sizing: Update `width`, `height`, `font-size` values
- Modify button styles: Edit the `.btn` class styles

## 📖 Additional Learning

To learn more about the technologies used:

- [Svelte 5 Documentation](https://svelte.dev/docs/svelte/overview)
- [Svelte Tutorial](https://learn.svelte.dev/)
- [Vite Documentation](https://vitejs.dev/)

## 🤝 Contributing

This is a learning project! Feel free to:
- Report bugs
- Suggest improvements
- Add new features
- Improve documentation

## 📄 License

This project is open source and available for educational purposes.

## 🙏 Acknowledgments

- Built with [Svelte 5](https://svelte.dev/)
- Powered by [Vite](https://vitejs.dev/)
- Inspired by classic calculator designs
