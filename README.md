# Porsche SPARK - Sales Training Course Platform

A Vue.js-based web application for Porsche sales training courses, designed to provide an interactive and engaging learning experience for sales professionals.

## 🚗 Overview

Porsche SPARK is a modern web application built with Vue 3 and Vite, featuring a sleek design inspired by Porsche's brand aesthetics. The platform delivers comprehensive sales training content with an intuitive user interface and responsive design.

## ✨ Features

- **Modern UI/UX**: Clean, professional interface following Porsche brand guidelines
- **Responsive Design**: Fully responsive layout that works on desktop, tablet, and mobile devices
- **Fast Performance**: Built with Vite for lightning-fast HMR and optimized production builds
- **Vue 3 Composition API**: Leveraging the latest Vue.js features for better performance and developer experience
- **Modular Architecture**: Well-organized component structure for easy maintenance and scalability

## 🛠️ Technology Stack

- **Frontend Framework**: Vue.js 3.4.38
- **Build Tool**: Vite 5.2.0
- **Development Language**: JavaScript (ES6+)
- **Styling**: Modern CSS with responsive design
- **Package Manager**: npm

## 📦 Installation

### Prerequisites

- Node.js (version 16 or higher)
- npm (version 7 or higher)

### Setup Instructions

1. Clone the repository:
```bash
git clone https://github.com/wukeping2008/porchespark.git
cd porchespark
```

2. Install dependencies:
```bash
npm install
```

3. Run the development server:
```bash
npm run dev
```

4. Open your browser and navigate to `http://localhost:5173`

## 🚀 Deployment

### Building for Production

```bash
npm run build
```

This command will generate optimized production files in the `dist/` directory.

### Deployment Configuration

The application is configured to be deployed at a subdirectory path `/porchespark/`. This is set in `vite.config.js`:

```javascript
export default defineConfig({
  plugins: [vue()],
  base: '/porchespark/',
});
```

### Deploying to a Web Server

1. Build the project using `npm run build`
2. Upload the contents of the `dist/` folder to your web server
3. Configure your web server (nginx/Apache) to serve the application from the `/porchespark/` path

#### Example nginx Configuration

```nginx
location /porchespark {
    alias /var/www/html/porchespark;
    try_files $uri $uri/ /porchespark/index.html;
    index index.html;
}
```

## 📁 Project Structure

```
porchespark/
├── dist/               # Production build files
├── public/             # Static assets
│   ├── porsche-911.png
│   ├── porsche-cayenne.png
│   ├── porsche-logo.png
│   └── porsche-wordmark.svg
├── src/                # Source code
│   ├── App.vue        # Main application component
│   └── main.js        # Application entry point
├── index.html          # HTML template
├── package.json        # Project dependencies and scripts
├── vite.config.js      # Vite configuration
└── README.md          # This file
```

## 🔧 Available Scripts

- `npm run dev` - Start the development server with hot-reload
- `npm run build` - Build the application for production
- `npm run preview` - Preview the production build locally

## 🌐 Live Demo

The application is deployed and available at:
- https://inspire.long-arena.com/porchespark/

## 📄 License

This project is proprietary and confidential. All rights reserved.

## 👥 Contributing

This is a private project. Please contact the repository owner for contribution guidelines.

## 📧 Contact

For questions or support, please contact the repository owner.

## 🙏 Acknowledgments

- Porsche AG for brand assets and guidelines
- Vue.js team for the excellent framework
- Vite team for the blazing fast build tool

---

Built with ❤️ for Porsche sales excellence