# Project Context Workflow

This workflow provides project-specific command guidance and context based on the centralized configuration.

## Step 1: Load Project Configuration

```xml
<read_file>
<path>.clinerules/repo-config.json</path>
</read_file>
```

## Step 2: Determine Current Context

Based on the current working directory and task context, provide relevant project-specific guidance.

## Project-Specific Commands

### Mobile Development
- **Run Android**: `yarn android` (from root directory, not packages/mobile)
- **Run iOS**: `yarn ios` (from root directory, not packages/mobile)  
- **Install Mobile Package**: `npx expo install <package>` (from packages/mobile directory)
- **Mobile Workspace**: `yarn mobile <command>` for workspace delegation

### Workspace Commands
- **Mobile**: `yarn mobile <script>` or `yarn workspace @wellness-planner/mobile <script>`
- **Functions**: `yarn functions <script>` or `yarn workspace @wellness-planner/functions <script>`
- **Shared**: `yarn shared <script>` or `yarn workspace @wellness-planner/shared <script>`
- **Conversation Tester**: `yarn tester <script>`

### Development Environment
- **Start Dev Environment**: `yarn dev` (runs development environment script)
- **Start Emulators**: `yarn emulators` (Firebase emulators for local development)
- **Deploy Functions**: `yarn deploy:functions` (production deployment)

### Build Commands
- **Build Shared**: `yarn build:shared` (build shared package)
- **Build Functions**: `yarn build:functions` (build functions package)
- **Prepare Functions Deploy**: `yarn prepare-functions-deploy` (full deployment preparation)

## Context-Aware Guidance

### When Working in Mobile Context (`packages/mobile/`)
- Use `npx expo install` for new packages
- Run commands from root with `yarn android` or `yarn ios`
- Use workspace commands: `yarn mobile <script>`

### When Working in Functions Context (`packages/functions/`)
- Use `yarn functions <script>` for function-specific commands
- Deploy with `yarn deploy:functions`
- Test locally with `yarn emulators`

### When Working in Shared Context (`packages/shared/`)
- Build shared package with `yarn build:shared` 
- Use `yarn shared <script>` for shared-specific commands

### When Installing Dependencies
- **Mobile packages**: Use `npx expo install` from `packages/mobile/`
- **Functions packages**: Use `yarn add` from `packages/functions/`
- **Shared packages**: Use `yarn add` from `packages/shared/`
- **Root dependencies**: Use `yarn add` from root

## Common Patterns

### Starting Development
1. Start emulators: `yarn emulators`
2. In another terminal: `yarn dev`
3. For mobile testing: `yarn android` or `yarn ios`

### Adding New Features
1. Determine which workspace the feature belongs to
2. Use appropriate package installation method
3. Follow workspace-specific development patterns
4. Test with relevant commands

### Deployment Preparation
1. Build shared: `yarn build:shared`
2. Build functions: `yarn build:functions`
3. Prepare deployment: `yarn prepare-functions-deploy`
4. Deploy: `yarn deploy:functions`

## Guidelines

- Always use project-specific commands from the configuration
- Consider workspace structure when suggesting commands
- Use Expo-managed installation for mobile packages
- Prefer yarn workspace commands for cross-package operations
