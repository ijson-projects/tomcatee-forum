# 🤝 Contributing to TomcatEE

Thank you for your interest in contributing to TomcatEE! This guide will help you get started with contributing to the project.

## 🎯 Ways to Contribute

### 📝 Documentation
- Improve existing documentation
- Create new tutorials and guides
- Translate content to other languages
- Fix typos and grammatical errors

### 🐛 Bug Reports
- Report bugs and issues
- Provide detailed reproduction steps
- Test and verify bug fixes

### 💡 Feature Requests
- Suggest new features
- Provide use cases and requirements
- Participate in feature discussions

### 💻 Code Contributions
- Fix bugs and issues
- Implement new features
- Improve performance
- Add tests and improve coverage

### 🤝 Community Support
- Answer questions in discussions
- Help other users troubleshoot issues
- Share best practices and tips
- Provide feedback on proposals

## 🚀 Getting Started

### Prerequisites

Before contributing, ensure you have:

- **Node.js** 16+ installed
- **npm** or **yarn** package manager
- **Git** for version control
- **VSCode** for development
- **Java** 8+ for testing
- **Apache Tomcat** for testing

### Development Setup

1. **Fork the Repository**
   ```bash
   # Fork on GitHub, then clone your fork
   git clone https://github.com/your-username/tomcatee.git
   cd tomcatee
   ```

2. **Install Dependencies**
   ```bash
   npm install
   ```

3. **Build the Extension**
   ```bash
   npm run compile
   ```

4. **Run Tests**
   ```bash
   npm test
   ```

5. **Start Development**
   - Open the project in VSCode
   - Press `F5` to launch Extension Development Host
   - Test your changes in the development environment

## 📋 Development Guidelines

### Code Style

We follow TypeScript and JavaScript best practices:

```typescript
// Use TypeScript for all new code
interface TomcatInstance {
    id: string;
    name: string;
    status: InstanceStatus;
}

// Use async/await for asynchronous operations
async function startInstance(instanceId: string): Promise<void> {
    try {
        const instance = await instanceManager.getInstance(instanceId);
        await instance.start();
    } catch (error) {
        console.error('Failed to start instance:', error);
        throw error;
    }
}

// Use proper error handling
class TomcatError extends Error {
    constructor(message: string, public readonly code: string) {
        super(message);
        this.name = 'TomcatError';
    }
}
```

### Project Structure

```
tomcatee/
├── src/                    # Source code
│   ├── extension.ts        # Extension entry point
│   ├── services/          # Business logic services
│   ├── models/            # Data models and interfaces
│   ├── webview/           # WebView components
│   └── utils/             # Utility functions
├── templates/             # HTML templates
├── test/                  # Test files
├── docs/                  # Documentation
└── package.json           # Extension manifest
```

### Coding Standards

1. **Use TypeScript** for all new code
2. **Follow ESLint rules** configured in the project
3. **Write unit tests** for new functionality
4. **Document public APIs** with JSDoc comments
5. **Use meaningful variable names** and function names
6. **Keep functions small** and focused on single responsibility

### Testing Guidelines

```typescript
// Example test structure
describe('TomcatInstanceManager', () => {
    let instanceManager: TomcatInstanceManager;
    
    beforeEach(() => {
        instanceManager = new TomcatInstanceManager();
    });
    
    describe('createInstance', () => {
        it('should create a new instance with valid configuration', async () => {
            const config = createValidConfig();
            const instance = await instanceManager.createInstance(config);
            
            expect(instance).toBeDefined();
            expect(instance.getId()).toBe(config.id);
            expect(instance.getName()).toBe(config.name);
        });
        
        it('should throw error for invalid configuration', async () => {
            const invalidConfig = createInvalidConfig();
            
            await expect(instanceManager.createInstance(invalidConfig))
                .rejects.toThrow('Invalid configuration');
        });
    });
});
```

## 🔄 Contribution Workflow

### 1. Planning

Before starting work:

1. **Check existing issues** to avoid duplication
2. **Create or comment on an issue** to discuss your proposal
3. **Wait for feedback** from maintainers
4. **Get approval** before starting significant work

### 2. Development

1. **Create a feature branch**
   ```bash
   git checkout -b feature/your-feature-name
   git checkout -b fix/issue-number
   ```

2. **Make your changes**
   - Follow coding standards
   - Write tests for new functionality
   - Update documentation as needed

3. **Test thoroughly**
   ```bash
   npm run compile
   npm test
   npm run lint
   ```

4. **Commit your changes**
   ```bash
   git add .
   git commit -m "feat: add new feature description"
   ```

### 3. Submission

1. **Push to your fork**
   ```bash
   git push origin feature/your-feature-name
   ```

2. **Create Pull Request**
   - Use descriptive title and description
   - Reference related issues
   - Include screenshots for UI changes
   - Add tests and documentation

3. **Respond to feedback**
   - Address review comments
   - Make requested changes
   - Update tests and documentation

## 📝 Pull Request Guidelines

### PR Title Format

Use conventional commit format:
- `feat: add new feature`
- `fix: resolve issue with startup`
- `docs: update configuration guide`
- `test: add tests for deployment`
- `refactor: improve code structure`

### PR Description Template

```markdown
## Description
Brief description of changes

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Documentation update
- [ ] Performance improvement
- [ ] Code refactoring

## Testing
- [ ] Unit tests pass
- [ ] Integration tests pass
- [ ] Manual testing completed

## Screenshots (if applicable)
Add screenshots for UI changes

## Related Issues
Fixes #123
Relates to #456

## Checklist
- [ ] Code follows project style guidelines
- [ ] Self-review completed
- [ ] Tests added/updated
- [ ] Documentation updated
- [ ] No breaking changes (or documented)
```

### Review Process

1. **Automated Checks**
   - Build verification
   - Test execution
   - Code quality checks
   - Security scanning

2. **Code Review**
   - Maintainer review
   - Community feedback
   - Requested changes

3. **Approval and Merge**
   - Final approval from maintainers
   - Merge to main branch
   - Release planning

## 🐛 Bug Reports

### Bug Report Template

When reporting bugs, include:

```markdown
## Bug Description
Clear description of the bug

## Steps to Reproduce
1. Step one
2. Step two
3. Step three

## Expected Behavior
What should happen

## Actual Behavior
What actually happens

## Environment
- TomcatEE Version: x.x.x
- VSCode Version: x.x.x
- Operating System: Windows/macOS/Linux
- Java Version: x.x.x
- Tomcat Version: x.x.x

## Additional Context
- Error messages
- Log files
- Screenshots
- Configuration details
```

### Bug Triage Process

1. **Initial Review** - Maintainers review and label
2. **Reproduction** - Attempt to reproduce the issue
3. **Investigation** - Analyze root cause
4. **Assignment** - Assign to contributor
5. **Resolution** - Fix and test
6. **Verification** - Verify fix works

## 💡 Feature Requests

### Feature Request Template

```markdown
## Feature Description
Clear description of the proposed feature

## Use Case
Why is this feature needed?

## Proposed Solution
How should this feature work?

## Alternatives Considered
Other approaches considered

## Additional Context
- Mockups or designs
- Related features
- Implementation ideas
```

### Feature Development Process

1. **Discussion** - Community discussion and feedback
2. **Design** - Technical design and planning
3. **Approval** - Maintainer approval
4. **Implementation** - Development work
5. **Testing** - Comprehensive testing
6. **Documentation** - User documentation
7. **Release** - Include in next release

## 🏷️ Issue Labels

We use labels to categorize issues:

- **Type**: `bug`, `feature`, `documentation`, `question`
- **Priority**: `low`, `medium`, `high`, `critical`
- **Status**: `needs-triage`, `in-progress`, `blocked`, `ready-for-review`
- **Area**: `ui`, `core`, `deployment`, `debugging`, `configuration`
- **Difficulty**: `good-first-issue`, `help-wanted`, `expert-needed`

## 🎯 Development Roadmap

### Current Focus Areas

1. **Performance Optimization**
   - Faster startup times
   - Improved hot deployment
   - Memory usage optimization

2. **User Experience**
   - Better error messages
   - Improved UI/UX
   - Enhanced documentation

3. **Platform Support**
   - Better Windows support
   - macOS ARM support
   - Linux distribution compatibility

4. **Integration**
   - Better IDE integration
   - CI/CD pipeline support
   - Cloud deployment options

### How to Get Involved

1. **Check the roadmap** in GitHub Projects
2. **Join discussions** about upcoming features
3. **Volunteer for specific areas** you're interested in
4. **Propose new initiatives** that align with project goals

## 📞 Getting Help

### Development Support

- 💬 **General Discussion**: [Community Forum](../../discussions)
- 🔧 **Development Help**: [Development Category](../../discussions/categories/development)
- 📧 **Direct Contact**: Reach out to maintainers for complex issues

### Resources

- **Project Documentation**: [User Guides](../user-guides/)
- **Technical Documentation**: [Technical Docs](../technical-docs/)
- **API Reference**: Generated from source code
- **Architecture Overview**: [Project Structure](../technical-docs/project-structure.md)

## 🙏 Recognition

Contributors are recognized through:

- **Contributors List** in README
- **Release Notes** acknowledgments
- **Community Highlights** in discussions
- **Maintainer Nominations** for significant contributors

---

**Thank you for contributing to TomcatEE! Together we can make Java web development more productive and enjoyable. 🚀**
