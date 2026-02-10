# json-form-builder

A web-based tool to build forms that export JSON data. This application uses a serverless architecture where form configurations are stored entirely within the URL parameters.

## Features

- **UI Builder**: Create form fields via a visual interface.
- **URL-Based Sharing**: Form schemas are encoded into the URL. No database or account is required.
- **JSON Export**: Fillers can copy their responses as raw JSON data.
- **Local Storage**: Your created forms are saved to your browser's local storage for future access.

## Tech Stack

- **Framework**: Svelte 5
- **Styling**: Tailwind CSS
- **Icons**: Lucide Svelte
- **Package Manager**: pnpm

## Getting Started

### Prerequisites

Ensure you have Node.js and pnpm installed on your machine.

### Installation

1. Clone the repository:

```bash
git clone https://github.com/moondip/json-form-builder.git

```

2. Install dependencies:

```bash
pnpm install

```

### Development

Start the development server:

```bash
pnpm dev

```

### Building

To create a production build:

```bash
pnpm build

```

You can preview the build with:

```bash
pnpm preview

```
