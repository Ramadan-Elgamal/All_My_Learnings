#!/bin/bash

# =============================================================================
# Generic React Project Structure - Reusable for ANY Project
# =============================================================================
# This is a TEMPLATE script that creates the standard React folder structure
# Use this for ANY future React project
# =============================================================================

echo "🚀 Creating generic React project structure..."
echo ""

# Color codes for output
GREEN='\033[0;32m'
BLUE='\033[0;34m'
NC='\033[0m' # No Color

# ============= CREATE MAIN FOLDERS =============
echo -e "${BLUE}📁 Creating main src/ folders...${NC}"

mkdir -p src/components
mkdir -p src/pages
mkdir -p src/hooks
mkdir -p src/utils
mkdir -p src/types
mkdir -p src/lib
mkdir -p src/context
mkdir -p src/assets/images
mkdir -p src/assets/icons
mkdir -p src/styles

# ============= CREATE SUB-FOLDERS IN COMPONENTS =============
echo -e "${BLUE}📁 Creating components sub-folders...${NC}"

mkdir -p src/components/layout
mkdir -p src/components/common
mkdir -p src/components/features
mkdir -p src/components/ui

# ============= CREATE CONFIG FOLDERS =============
echo -e "${BLUE}📁 Creating config folders...${NC}"

mkdir -p config
mkdir -p public

# ============= CREATE INDEX FILES =============
echo -e "${BLUE}📝 Creating index.ts files...${NC}"

# src/components/index.ts
cat > src/components/index.ts << 'EOF'
// Layout components
export * from './layout';

// Common components
export * from './common';

// Feature components
export * from './features';

// UI components
export * from './ui';
EOF

# src/components/layout/index.ts
cat > src/components/layout/index.ts << 'EOF'
// Layout components
// Example: export { Layout } from './Layout';
EOF

# src/components/common/index.ts
cat > src/components/common/index.ts << 'EOF'
// Common/reusable components
// Example: export { Button } from './Button';
// Example: export { Header } from './Header';
EOF

# src/components/features/index.ts
cat > src/components/features/index.ts << 'EOF'
// Feature-specific components
// Example: export { TaskCard } from './TaskCard';
EOF

# src/components/ui/index.ts
cat > src/components/ui/index.ts << 'EOF'
// shadcn/ui components will be auto-generated here
// You can also add custom UI components
EOF

# src/hooks/index.ts
cat > src/hooks/index.ts << 'EOF'
// Custom React hooks
// Example: export { useData } from './useData';
// Example: export { useAuth } from './useAuth';
EOF

# src/utils/index.ts
cat > src/utils/index.ts << 'EOF'
// Utility functions
// Example: export { formatDate } from './formatDate';
// Example: export { cn } from './cn';
EOF

# src/types/index.ts
cat > src/types/index.ts << 'EOF'
// TypeScript type definitions
// Define your domain models here
EOF

# src/lib/index.ts
cat > src/lib/index.ts << 'EOF'
// Third-party library setup and configuration
// Example: Database client
// Example: API client
// Example: Authentication service
EOF

# src/context/index.ts
cat > src/context/index.ts << 'EOF'
// React Context providers
// Example: export { AuthProvider } from './AuthContext';
// Example: export { useAuth } from './useAuth';
EOF

# src/styles/index.css
cat > src/styles/index.css << 'EOF'
/* Global styles */
/* Import Tailwind CSS and custom styles here */
EOF

# ============= CREATE README FILES =============
echo -e "${BLUE}📄 Creating README files...${NC}"

# src/components/README.md
cat > src/components/README.md << 'EOF'
# Components

## Structure

- **layout/** - Layout wrapper components
- **common/** - Reusable components
- **features/** - Feature-specific components
- **ui/** - shadcn/ui or custom UI components

## Guidelines

1. Single responsibility per component
2. Well-typed props with TypeScript interfaces
3. Use barrel exports (index.ts) for clean imports
4. Keep components small and focused
EOF

# src/hooks/README.md
cat > src/hooks/README.md << 'EOF'
# Custom Hooks

Store all custom React hooks here.

## Guidelines

- Hook names should start with "use"
- Keep hooks focused on single concern
- Document what the hook does
- Return clear, typed values
EOF

# src/utils/README.md
cat > src/utils/README.md << 'EOF'
# Utility Functions

Pure functions for common tasks.

## Categories

- **Formatting** - format data for display
- **Validation** - validate user input
- **Helpers** - common algorithms
- **CSS** - CSS utilities like cn()
EOF

# src/types/README.md
cat > src/types/README.md << 'EOF'
# TypeScript Types

All type definitions for the application.

## Guidelines

- Use interfaces for object types
- Use enums for fixed value sets
- Prefix component props with component name
- Document complex types with comments
EOF

# src/lib/README.md
cat > src/lib/README.md << 'EOF'
# Library Configuration

Third-party service setup and configuration.

## Guidelines

- Initialize services here
- Export configured instances
- Keep secrets in environment variables
EOF

# src/context/README.md
cat > src/context/README.md << 'EOF'
# React Context

Global state management with Context API.

## Guidelines

- Keep context focused on one concern
- Create custom hooks to use context
- Document context structure
EOF

# ============= CREATE .GITKEEP FILES =============
echo -e "${BLUE}🔒 Creating .gitkeep files...${NC}"

touch src/components/.gitkeep
touch src/pages/.gitkeep
touch src/hooks/.gitkeep
touch src/utils/.gitkeep
touch src/context/.gitkeep
touch src/assets/images/.gitkeep
touch src/assets/icons/.gitkeep

# ============= COMPLETION MESSAGE =============
echo ""
echo -e "${GREEN}✅ GENERIC STRUCTURE SETUP COMPLETE!${NC}"
echo ""
echo "📁 Folder structure created:"
echo ""
echo "src/"
echo "├── components/"
echo "│   ├── layout/"
echo "│   ├── common/"
echo "│   ├── features/"
echo "│   ├── ui/"
echo "│   └── index.ts"
echo "├── pages/"
echo "├── hooks/"
echo "│   └── index.ts"
echo "├── utils/"
echo "│   └── index.ts"
echo "├── types/"
echo "│   └── index.ts"
echo "├── lib/"
echo "│   └── index.ts"
echo "├── context/"
echo "│   └── index.ts"
echo "├── assets/"
echo "│   ├── images/"
echo "│   └── icons/"
echo "└── styles/"
echo ""
echo "🎯 Now you can:"
echo "   1. Add project-specific types"
echo "   2. Create your first component"
echo "   3. Set up your hooks"
echo ""
echo "🔄 Or run the project-specific script to populate with samples!"