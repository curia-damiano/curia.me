# curia.me

Personal blog powered by Hugo and hosted on GitHub Pages.

## Overview

This repository contains the source code for [curia.me](https://curia.me), a static blog built with Hugo and deployed as GitHub Pages.

## Development

### Prerequisites

- [Hugo](https://gohugo.io/) (extended version recommended)
- Git

### Getting Started

1. Clone the repository with submodules:

   ```bash
   git clone --recurse-submodules https://github.com/curia-damiano/curia.me.git
   cd curia.me
   ```

   If you already cloned without submodules, run:

   ```bash
   git submodule update --init --recursive
   ```

2. Start the Hugo development server:

   ```bash
   hugo server -D
   ```

3. Visit `http://localhost:1313` to preview your site

### Development with VS Code & Dev Containers (Recommended)

This project is configured for development using Visual Studio Code with Dev Containers, which provides a consistent development environment with all dependencies pre-installed.

**Requirements:**

- [Visual Studio Code](https://code.visualstudio.com/)
- [Docker](https://www.docker.com/)
- [Dev Containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

**To get started:**

1. Open the project in VS Code
2. When prompted, click "Reopen in Container" (or use Command Palette: `Dev Containers: Reopen in Container`)
3. VS Code will build and start the dev container with Hugo, Node.js, and other tools pre-configured
4. Start developing immediately without manual setup!

## Building

Generate the static site:

```bash
hugo
```

The site will be built to the `public/` directory.

## Deployment

The site is automatically deployed to GitHub Pages. Push changes to the main branch, and GitHub Actions will build and deploy the site.

## Project Structure

```text
.
├── archetypes/     # Content templates
├── content/        # Blog posts and pages
├── layouts/        # HTML templates
├── static/         # Static assets (images, CSS, JS)
├── themes/         # Hugo themes
└── config.toml     # Hugo configuration
```

## License

See [LICENSE](LICENSE) file for details.
