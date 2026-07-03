### Phase 0 - Plan & Design
- Generate the `PRD` file for the project. [[prd_prompt]] .
- Generate the `User Stories` . [[user-stories-prompts]] .
- Generate the `design.md` using `Stitch` .

### PHASE 1 - Foundation
- Generate the Database schema.
- Use [[setup-script.sh]] to create the folder structure.
- Translate the database schema into types and interfaces and add it to the `types/index.ts` floder with other reusable types 
- Implement the r

### PHASE 2 - Backend Foundation
- Choose auth provider (Clerk, Auth0, etc.)
- Integrate it into app 
- Create useAuth hook - Protect routes - Create login/signup pages - Test auth flow end-to-end

### PHASE 3: UI Components
- Theming & Styling ( Dark mode support - Light mode support - Theme toggle)
- Create reusable components ( Button variants - Input components - Card/Container components - Modal/Dialog components - Headers/Navigation - Footers - Loaders/Skeletons 
- Build Feature Components ( Domain-specific components - Feature-based organization - Connect to API - Use typed props - Handle loading states - Handle error states)
- Build Page Components ( Combine features into pages - Setup routing - Layout structure - Navigation between pages - Test navigation flow)