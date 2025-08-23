# Biome (ESLint + Prettier Replacement)

A modern, fast, and simple alternative to ESLint + Prettier using Biome.

## What's included?

- Standard config base
- Full React and React Hooks support
- Accessibility (a11y) rules
- Integrated formatting (replaces Prettier)
- Native TypeScript support
- Automatic import organization
- **Up to 100x faster performance** than ESLint + Prettier

## Setup

### React (with Next.js)

Install dependencies:

```bash
npm i -D @biomejs/biome
```

Create `biome.json`:

```json
{
  "$schema": "https://biomejs.dev/schemas/1.9.4/schema.json",
  "formatter": {
    "enabled": true,
    "formatWithErrors": false,
    "indentStyle": "space",
    "indentWidth": 2,
    "lineWidth": 80,
    "lineEnding": "lf"
  },
  "javascript": {
    "formatter": {
      "quoteStyle": "single",
      "trailingCommas": "all",
      "semicolons": "asNeeded",
      "arrowParentheses": "always",
      "jsxQuoteStyle": "double"
    }
  },
  "linter": {
    "enabled": true,
    "rules": {
      "recommended": true,
      "correctness": {
        "noUnusedVariables": "error",
        "noUnusedImports": "error",
        "useExhaustiveDependencies": "warn",
        "useHookAtTopLevel": "error"
      },
      "style": {
        "noUnusedTemplateLiteral": "error",
        "useImportType": "error",
        "useConsistentArrayType": "error",
        "useSelfClosingElements": "error",
        "useFragmentSyntax": "error"
      },
      "suspicious": {
        "noExplicitAny": "warn",
        "noArrayIndexKey": "warn"
      },
      "a11y": {
        "recommended": true,
        "useAltText": "warn",
        "useAriaProps": "warn",
        "useValidAriaProps": "warn",
        "useValidAriaRole": "warn",
        "useKeyWithClickEvents": "warn",
        "useKeyWithMouseEvents": "warn",
        "noBlankTarget": "error"
      },
      "complexity": {
        "noForEach": "off"
      }
    }
  },
  "organizeImports": {
    "enabled": true
  },
  "files": {
    "include": ["**/*.js", "**/*.jsx", "**/*.ts", "**/*.tsx"],
    "ignore": [
      "node_modules/**", 
      "dist/**", 
      "build/**", 
      "coverage/**", 
      ".next/**",
      "out/**",
      "public/**"
    ]
  },
  "overrides": [
    {
      "includes": ["pages/**", "app/**"],
      "linter": {
        "rules": {
          "style": {
            "useFilenamingConvention": "off"
          }
        }
      }
    }
  ]
}
```

### React (without Next.js)

Install dependencies:

```bash
npm i -D @biomejs/biome
```

Create `biome.json`:

```json
{
  "$schema": "https://biomejs.dev/schemas/1.9.0/schema.json",
  "formatter": {
    "enabled": true,
    "formatWithErrors": false,
    "indentStyle": "space",
    "indentWidth": 2,
    "lineWidth": 80,
    "lineEnding": "lf"
  },
  "javascript": {
    "formatter": {
      "quoteStyle": "single",
      "trailingCommas": "es5",
      "semicolons": "asWhenNeeded",
      "arrowParentheses": "always",
      "jsxQuoteStyle": "double"
    }
  },
  "linter": {
    "enabled": true,
    "rules": {
      "recommended": true,
      "correctness": {
        "noUnusedVariables": "error",
        "noUnusedImports": "error",
        "useExhaustiveDependencies": "warn"
      },
      "style": {
        "noUnusedTemplateLiteral": "error",
        "useImportType": "error",
        "useConsistentArrayType": "error",
        "useSelfClosingElements": "error"
      },
      "suspicious": {
        "noExplicitAny": "warn",
        "noArrayIndexKey": "error"
      },
      "a11y": {
        "recommended": true,
        "noBlankTarget": "error",
        "useAltText": "error",
        "useAriaLabel": "error",
        "useValidAriaProps": "error"
      },
      "complexity": {
        "noForEach": "off"
      }
    }
  },
  "organizeImports": {
    "enabled": true
  },
  "files": {
    "include": ["**/*.js", "**/*.jsx", "**/*.ts", "**/*.tsx"],
    "ignore": ["node_modules/**", "dist/**", "build/**", "coverage/**"]
  }
}
```

### Node.js

Install dependencies:

```bash
npm i -D @biomejs/biome
```

Create `biome.json`:

```json
{
  "$schema": "https://biomejs.dev/schemas/1.9.0/schema.json",
  "formatter": {
    "enabled": true,
    "formatWithErrors": false,
    "indentStyle": "space",
    "indentWidth": 2,
    "lineWidth": 80,
    "lineEnding": "lf"
  },
  "javascript": {
    "formatter": {
      "quoteStyle": "single",
      "trailingCommas": "es5",
      "semicolons": "asWhenNeeded",
      "arrowParentheses": "always"
    }
  },
  "linter": {
    "enabled": true,
    "rules": {
      "recommended": true,
      "correctness": {
        "noUnusedVariables": "error",
        "noUnusedImports": "error"
      },
      "style": {
        "noUnusedTemplateLiteral": "error",
        "useImportType": "error",
        "useConsistentArrayType": "error",
        "useForOf": "error"
      },
      "suspicious": {
        "noExplicitAny": "warn",
        "noArrayIndexKey": "off"
      },
      "complexity": {
        "noForEach": "off"
      }
    }
  },
  "organizeImports": {
    "enabled": true
  },
  "files": {
    "include": ["**/*.js", "**/*.ts", "**/*.mjs"],
    "ignore": ["node_modules/**", "dist/**", "build/**", "coverage/**"]
  }
}
```

## Recommended Scripts

Add to your `package.json`:

```json
{
  "scripts": {
    "lint": "biome check .",
    "lint:fix": "biome check --write .",
    "format": "biome format --write .",
    "format:check": "biome format ."
  }
}
```

## Useful Commands

```bash
# Check code (lint + format)
npm run lint

# Auto-fix issues
npm run lint:fix

# Format only
npm run format

# Check formatting without changes
npm run format:check

# Organize imports only
biome check --write --only=organizeImports .
```

## Migration from ESLint + Prettier

If you already have ESLint and Prettier configured:

```bash
# Remove old dependencies
npm uninstall eslint prettier @typescript-eslint/eslint-plugin @typescript-eslint/parser eslint-plugin-react eslint-plugin-react-hooks eslint-plugin-jsx-a11y eslint-config-prettier eslint-plugin-prettier @rocketseat/eslint-config

# Remove config files
rm .eslintrc.json .prettierrc .prettierignore

# Install Biome
npm install -D @biomejs/biome

# Create biome.json with one of the configurations above
```

## Advantages vs ESLint + Prettier

- ⚡ **100x faster** - written in Rust
- 🔧 **Single tool** - linting + formatting + import organization
- 📦 **Fewer dependencies** - no need for dozens of plugins
- ⚙️ **Simple configuration** - one JSON file
- 🚀 **Zero configuration** - works out-of-the-box
- 🔄 **Consistent formatting** - no conflicts between linter and formatter

## VS Code Integration

Install the official Biome extension:
- **Biome** - biomejs.biome

Configuration in `settings.json`:

```json
{
  "editor.defaultFormatter": "biomejs.biome",
  "editor.formatOnSave": true,
  "editor.codeActionsOnSave": {
    "quickfix.biome": "explicit",
    "source.organizeImports.biome": "explicit"
  }
}
```
