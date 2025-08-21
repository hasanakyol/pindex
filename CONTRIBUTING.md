# Contributing to Pindex

First off, thank you for considering contributing to Pindex! It's people like you that make Pindex such a great tool.

## Code of Conduct

This project and everyone participating in it is governed by our Code of Conduct. By participating, you are expected to uphold this code.

## How Can I Contribute?

### Reporting Bugs

Before creating bug reports, please check existing issues as you might find out that you don't need to create one. When you are creating a bug report, please include as many details as possible:

* Use a clear and descriptive title
* Describe the exact steps which reproduce the problem
* Provide specific examples to demonstrate the steps
* Describe the behavior you observed after following the steps
* Explain which behavior you expected to see instead and why
* Include details about your configuration and environment

### Suggesting Enhancements

Enhancement suggestions are tracked as GitHub issues. When creating an enhancement suggestion, please include:

* Use a clear and descriptive title
* Provide a step-by-step description of the suggested enhancement
* Provide specific examples to demonstrate the steps
* Describe the current behavior and explain which behavior you expected to see instead
* Explain why this enhancement would be useful

### Pull Requests

* Fill in the required template
* Do not include issue numbers in the PR title
* Follow the styleguides
* Include thoughtfully-worded, well-structured tests
* Document new code
* End all files with a newline

## Styleguides

### Git Commit Messages

* Use the present tense ("Add feature" not "Added feature")
* Use the imperative mood ("Move cursor to..." not "Moves cursor to...")
* Limit the first line to 72 characters or less
* Reference issues and pull requests liberally after the first line

### Documentation Styleguide

* Use [Markdown](https://daringfireball.net/projects/markdown)
* Reference commands using backticks: `/pin:plan`
* Use EARS format for requirements documentation

### Command Development

When adding new commands to the `/pin:` namespace:

1. Create the command file in `@.claude/commands/pin/`
2. Include proper frontmatter with description and allowed-tools
3. Follow the existing command structure pattern
4. Update the help.md file to include your new command
5. Add appropriate tests and documentation

## Project Structure

```
.claude/
├── commands/pin/     # Slash commands
├── templates/        # Document templates
└── CLAUDE.md        # Main documentation

features/            # Generated feature specifications
```

## Development Process

1. Fork the repo
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## Testing

* Ensure all commands work as expected
* Test with both new projects and existing codebases
* Verify EARS requirements generation
* Check TDD workflow implementation

## Questions?

Feel free to open an issue with your question or contact the maintainers directly.

Thank you for contributing! 🎉
