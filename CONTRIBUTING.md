# Contributing to the Neuroinformatics Unit Website

Thank you for your interest in contributing to the Neuroinformatics Unit website! We welcome contributions from the community.

## Quick Start

1. **Fork and Clone**: Fork this repository and clone it locally
2. **Create a Branch**: Create a new branch for your changes
3. **Make Changes**: Edit the website files in `docs/source/`
4. **Test Locally**: Build the site locally to verify your changes (see below)
5. **Submit PR**: Push your branch and create a pull request

## Local Development

### Build the Website Locally

```bash
# Install dependencies (only needed once)
pip install -r docs/requirements.txt

# Build the website
rm -rf docs/build  # remove existing local build
sphinx-build docs/source docs/build  # make new build
```

You can view the local build by opening `docs/build/index.html` in your browser.

## Development Guidelines

For detailed development guidelines, please see our comprehensive documentation:
- [Development Guidelines](https://neuroinformatics.dev/get-involved/development_guidelines.html)
- [AI Policy](https://neuroinformatics.dev/get-involved/ai_policy.html)

## Website Structure

The website is built using [Sphinx](https://www.sphinx-doc.org/en/master/) and the [PyData Sphinx Theme](https://pydata-sphinx-theme.readthedocs.io/en/latest/).

- Configuration: `docs/source/conf.py`
- Main page: `docs/source/index.md`
- Other pages: `docs/source/<page-name>.md` files

## Pull Request Process

1. Create a draft PR early to get feedback
2. Ensure your changes build successfully (GitHub Actions will verify this)
3. Request a review when ready
4. Address any review comments
5. Once approved, your PR will be merged and automatically deployed

## Code of Conduct

Please review our [Code of Conduct](https://neuroinformatics.dev/resources/code_of_conduct.html) before contributing.

## Questions?

If you have questions, feel free to:
- Open an issue on GitHub
- Join our [Zulip chat](https://neuroinformatics.zulipchat.com/)
- Check our [Get Involved](https://neuroinformatics.dev/get-involved/index.html) page

Thank you for contributing!
