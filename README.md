# MDMY Documentation

This repository contains the documentation site for MDMY Group, built with [MkDocs](https://www.mkdocs.org/) and the [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) theme.

## Getting Started

### Prerequisites

- Python 3.9 or higher
- pip (Python package manager)

### Installation

1. Clone this repository:
   ```bash
   git clone https://github.com/mdmy-group/mdmy-mkdocs.git
   cd mdmy-mkdocs
   ```

2. Create a virtual environment (optional but recommended):
   ```bash
   python -m venv venv
   
   # On Windows
   venv\Scripts\activate
   
   # On macOS/Linux
   source venv/bin/activate
   ```

3. Install the required dependencies:
   ```bash
   pip install -r requirements.txt
   ```

## Local Development

To run the documentation site locally:

```bash
mkdocs serve
```

This will start a development server at `http://127.0.0.1:8000/`. The site will automatically reload when you make changes to the content.

## Building the Static Site

To build the static site:

```bash
mkdocs build
```

This will create a `site` directory with the built static site.

## Deployment

### GitHub Pages

This repository is configured to automatically deploy to GitHub Pages when changes are pushed to the `main` branch using GitHub Actions.

### Manual Deployment

To manually deploy the site to GitHub Pages:

```bash
mkdocs gh-deploy --force
```

### Netlify Deployment

This repository also includes a `netlify.toml` file for easy deployment on Netlify. To deploy on Netlify:

1. Push the repository to GitHub
2. Connect the repository to Netlify
3. Netlify will automatically detect the configuration and build settings

## Documentation Structure

```
/docs
├── index.md              # Homepage
├── getting-started.md    # Getting started guide
├── about.md              # About page
├── /guides               # User guides section
│   ├── index.md          # Overview of guides
│   ├── guide-1.md        # Specific guides
│   ├── guide-2.md
├── /reference            # Reference documentation
│   ├── index.md          # Overview of reference docs
│   ├── api-reference.md  # API documentation
```

## Contributing

1. Create a new branch for your changes
2. Make your changes to the documentation
3. Submit a pull request for review

### Adding New Pages

1. Create a new Markdown file in the appropriate directory under `/docs`
2. Add the page to the navigation in `mkdocs.yml`

## License

Copyright © 2025 MDMY Group