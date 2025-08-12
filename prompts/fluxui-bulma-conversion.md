  Bulma to FluxUI Migration Prompt

  Context: I need to migrate a Laravel application from Bulma CSS framework to FluxUI (Livewire Flux). This app has FluxUI
  documentation available in fluxui-docs/ directory with the main guidance in fluxui-docs/GUIDENCE.md.

  Migration Approach:
  1. Start by reading fluxui-docs/GUIDENCE.md to understand FluxUI principles (simplicity, "We Style You Space", composition,
  etc.)
  2. Focus on templates only - do NOT convert routes to use Livewire components directly unless explicitly requested
  3. Work systematically: Layout first, then major components, then refinements

  Key FluxUI Conversion Patterns:

  Layout & Structure:
  - Remove complex sidebars for simple apps - use clean <main> with responsive containers
  - Use w-full md:w-3/4 mx-auto for main content containers (not too wide, not too narrow)
  - Move shared header elements (title, navigation buttons, logout) to layout files
  - Use <flux:separator class="mb-6" /> instead of <hr>

  Component Conversions:
  - table.table → <flux:table> with <flux:table.columns>, <flux:table.rows>, <flux:table.cell>
  - button.button → <flux:button> with appropriate variants (primary, danger, subtle)
  - input.input → <flux:input> with labels as props, use wire:model.live for filtering/search
  - field/control structures → Simple <flux:input label="Label"> or composable <flux:field> approach
  - Bulma columns/column → CSS Grid (grid grid-cols-1 lg:grid-cols-2 gap-6)
  - box classes → <flux:card> components
  - title/subtitle → <flux:heading> with appropriate sizes
  - Error messages → <flux:text variant="danger">

  UI Refinements:
  - Delete buttons: Make icon-only with icon="trash", variant="danger", size="sm", inset="top bottom" - remove text to be less
  aggressive
  - Search inputs: Constrain width with max-w-md wrapper, add magnifying glass icon
  - Input groups: Use iconTrailing slots for buttons attached to inputs, not separate button groups
  - Spacing: Use margin classes (mb-6, mt-4) for spacing between components following "We Style, You Space"

  Livewire Integration:
  - Ensure @livewireStyles in <head> and @livewireScripts before </body>
  - Remove .prevent modifiers from wire:click that may interfere with FluxUI buttons
  - Use wire:model.live for real-time filtering/search functionality
  - FluxUI components properly forward Livewire attributes

  Layout Responsiveness:
  - Start with max-w-5xl container widths, adjust if too wide/narrow
  - Use responsive grids that adapt based on content (e.g., notes panels)
  - Test on different screen sizes and adjust container widths as needed

  Common Issues & Solutions:
  - If Livewire functionality breaks: Check for missing scripts, remove .prevent modifiers
  - If layout looks too wide: Add responsive containers with appropriate max-widths
  - If buttons look too aggressive: Use icon-only delete buttons with subtle styling
  - If input groups look disconnected: Use FluxUI's iconTrailing slot pattern

  Testing Checklist:
  - All Livewire functionality works (buttons, filtering, forms)
  - Responsive design works on mobile and desktop
  - Delete buttons are appropriately subtle
  - Forms follow FluxUI patterns
  - Error handling displays properly
  - Layout feels balanced (not too wide or narrow)

  Approach: Work through templates systematically, test functionality after each conversion, and iterate on spacing/sizing based
   on visual feedback. Follow FluxUI documentation patterns exactly, and prioritize user experience improvements where possible.

