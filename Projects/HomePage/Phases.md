Here is the blueprint for your build process. It is structured to ensure the Vanguard design system is locked in before any components are built, preventing Tailwind or GSAP defaults from polluting the UI.

### Phase 1: Foundation & Design System Enforcement

The goal of this phase is to initialize the repository, install dependencies, and aggressively overwrite framework defaults with Vanguard’s strict tokens.

- `chore: init react vite project and install tailwind v4, gsap, zustand`
    
- `build: gut tailwind defaults and configure vanguard design tokens in css`
    
- `build: set global gsap default duration and easing to match vanguard motion spec`
    
- `feat(store): init zustand store with localstorage for workspace state`
    
- `chore(store): seed initial workspaces (software engineering, automation workflows, media)`
    

### Phase 2: Macro Layout & Structural Skeleton

This phase focuses on the CSS Grid architecture that maps out your command center regions without worrying about the micro-components inside them.

- `feat(layout): build root css grid for top bar, sidebar, and main dock`
    
- `feat(layout): implement global noise overlay and #050505 neutral background`
    
- `feat(components): scaffold empty structural containers (Sidebar, TopBar, MainFocus, BottomDock)`
    
- `style: apply vanguard glassy surface treatments to structural panels`
    

### Phase 3: Left Sidebar & Workspace Navigation

Here, we build the persistent left-hand navigation, utilizing the Vanguard `button-link` specs and wiring up the Zustand store to handle active contexts.

- `feat(ui): build reusable vanguard button-link component`
    
- `feat(sidebar): implement workspace switcher navigation list`
    
- `feat(sidebar): add quick launch pinned links block (github, laravel herd, n8n, etc.)`
    
- `style(sidebar): add #FF4F18 active state indicator and typography styling`
    
- `feat(store): wire sidebar navigation to zustand activeWorkspace state`
    

### Phase 4: Top Command Bar & Keyboard-First Architecture

This phase turns the dashboard into an "operating system" by implementing the global control center and the critical keyboard shortcuts.

- `feat(topbar): build glass topbar layout with flex rhythm`
    
- `feat(topbar): add system clock and workspace status indicators`
    
- `feat(cmd): build hidden command palette overlay structure`
    
- `feat(a11y): implement global keyboard event listener for shortcuts (Cmd+K, G+P)`
    
- `feat(cmd): wire Cmd+K to toggle command palette visibility via zustand`
    

### Phase 5: Main Focus Area & Hero Context

This is where the intentional asymmetry comes into play. We will build the high-density cards using the strict 2.25px radius and gradient shell techniques.

- `feat(main): build hero context card wrapper using gradient border shell technique`
    
- `feat(main): implement dynamic css grid for secondary widgets`
    
- `feat(widgets): build active project sprint widget for hero context`
    
- `feat(widgets): build local dev server status and recent activity widgets`
    
- `style(main): enforce 4.5px base spacing and layout flex within widgets`
    

### Phase 6: Motion, Transitions & Polish

The final phase injects the 600ms/1000ms expressive Vanguard motion and ensures the UI feels seamless when switching contexts.

- `feat(anim): add gsap opacity and transform entry animations on initial load`
    
- `feat(anim): implement workspace transition animations when switching contexts`
    
- `feat(anim): add hover motion patterns for text and color on interactive elements`
    
- `fix(style): audit and lock all corner radii to strictly 2.25px or 9999px`
    
- `docs: update readme with setup instructions and workspace configuration guide`