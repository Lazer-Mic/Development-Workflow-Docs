# Python Development Environment

## Overview
Python serves as one of our primary programming languages, used for automation, scripting, and general development tasks.

## Our Python Setup
- **Version Management**: Multiple Python versions via Homebrew
- **Virtual Environments**: venv for project isolation
- **Package Management**: pip for package installation
- **IDE Integration**: Python support in Cursor and VS Code
- **Development Tools**: Linting, formatting, and debugging tools

## Installation & Configuration
### Python Installation
```bash
# Install via Homebrew
brew install python

# Verify installation
python3 --version
pip3 --version
```

### Virtual Environment Setup
```bash
# Create virtual environment
python3 -m venv project-env

# Activate environment
source project-env/bin/activate

# Deactivate when done
deactivate
```

## Workflow Integration
- **Automation Scripts**: System and workflow automation
- **Data Processing**: File manipulation and data analysis
- **API Development**: Web service creation and consumption
- **Documentation Tools**: Integration with documentation workflows
- **System Administration**: macOS system management scripts

## Package Ecosystem
### Core Packages
- **requests**: HTTP library for API interactions
- **pathlib**: Modern file path handling
- **json**: JSON data processing
- **subprocess**: System command execution

### Development Tools
- **black**: Code formatting
- **flake8**: Code linting
- **pytest**: Testing framework
- **mypy**: Type checking

## Usage Patterns
### Project Structure
```
project/
├── venv/              # Virtual environment
├── src/               # Source code
├── tests/             # Test files
├── requirements.txt   # Dependencies
└── README.md         # Documentation
```

### Development Workflow
1. **Environment Setup**: Create and activate virtual environment
2. **Dependency Management**: Install packages via pip
3. **Code Development**: Write and test Python code
4. **Quality Assurance**: Linting and formatting
5. **Documentation**: Document code and usage

## Learning Journey
- **Starting Point**: Basic scripting for automation
- **Current Level**: Intermediate development with best practices
- **Focus Areas**: Clean code, testing, and documentation
- **Future Goals**: Advanced frameworks and web development

## Integration with Other Tools
- **Claude AI**: Python code assistance and learning
- **Git**: Version control for Python projects
- **mdBook**: Python scripts for documentation automation
- **Terminal**: Command-line Python development