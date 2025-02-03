# Contributing to Helm Charts Repository

We love your input! We want to make contributing to this Helm charts repository as easy and transparent as possible, whether it's:

- Reporting a bug in an existing chart
- Discussing the current state of a chart
- Submitting a fix
- Proposing new charts
- Becoming a maintainer

## Chart Development Process

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-chart`)
3. Create your chart in a new directory
4. Ensure your chart follows these guidelines:
   - Include a detailed README.md
   - Include a values.yaml with comments explaining each value
   - Include appropriate NOTES.txt
   - Follow [Helm best practices](https://helm.sh/docs/chart_best_practices/)
   - Version your chart appropriately (semantic versioning)

## Chart Structure

Each chart should have the following structure:

```
chart-name/
  ├── Chart.yaml
  ├── values.yaml
  ├── README.md
  ├── templates/
  │   ├── NOTES.txt
  │   ├── _helpers.tpl
  │   ├── deployment.yaml
  │   └── service.yaml
  └── charts/
```

## Chart Requirements

1. **Documentation**
   - Clear description in Chart.yaml
   - Comprehensive README.md
   - Well-commented values.yaml
   - Helpful NOTES.txt

2. **Testing**
   - Include basic tests
   - Test with different values
   - Document test cases

3. **Security**
   - Follow security best practices
   - Set appropriate default values
   - Document security considerations

## Pull Request Process

1. Update the README.md with details of changes if applicable
2. Update the Chart.yaml with the new version number
3. The PR will be merged once you have the sign-off of at least one maintainer

## Any contributions you make will be under the MIT Software License

In short, when you submit code changes, your submissions are understood to be under the same [MIT License](LICENSE) that covers the project. Feel free to contact the maintainers if that's a concern.

## Report bugs using Github's [issue tracker]

We use GitHub issues to track public bugs. Report a bug by [opening a new issue]().

## Write bug reports with detail, background, and sample code

**Great Bug Reports** tend to have:

- A quick summary and/or background
- Steps to reproduce
  - Be specific!
  - Give sample code if you can
- What you expected would happen
- What actually happens
- Notes (possibly including why you think this might be happening, or stuff you tried that didn't work)

## License

By contributing, you agree that your contributions will be licensed under its MIT License. 