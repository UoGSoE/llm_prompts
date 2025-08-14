  Older tailwind/laravel to FluxUI Migration Prompt

  Context: I need to migrate a Laravel application from an older plain livewire and tailwind CSS framework to FluxUI (Livewire Flux). This app has FluxUI
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
  - tables → <flux:table> with <flux:table.columns>, <flux:table.rows>, <flux:table.cell>
  - buttons → <flux:button> with appropriate variants (primary, danger, subtle)
  - inputs → <flux:input> with labels as props, use wire:model.live for filtering/search
  - field/control structures → Simple <flux:input label="Label"> or composable <flux:field> approach
  - columns/column → CSS Grid (grid grid-cols-1 lg:grid-cols-2 gap-6)
  - box classes → <flux:card> components
  - title/subtitle → <flux:heading> with appropriate sizes
  - Error messages → <flux:text variant="danger">

  FluxUI Attribute Binding Best Practice:

  Instead of using Blade directives in attributes:
  class="@if ($condition) some-classes @endif"

  Use Laravel's attribute binding syntax with ternary operators:
  :class="$condition ? 'some-classes' : ''"
  :title="$condition ? 'Some title' : ''"

  Why this is better:
  1. Cleaner syntax - More readable and less verbose
  2. Proper binding - Uses Laravel's native attribute binding (:attribute)
  3. Avoids parsing issues - Prevents Blade directive conflicts within HTML attributes
  4. FluxUI compatible - Flux components are designed to work with Laravel's binding syntax
  5. More maintainable - Ternary operators are easier to debug than nested Blade directives

  Key pattern to remember:
  - Use :attribute="expression" for dynamic values
  - Use ternary operators condition ? 'value-if-true' : 'value-if-false' for conditional content
  - This applies to all attributes: :class, :title, :disabled, :href, etc.

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
  - If the user is seeing errors about 'component not found' - try checking the directory 'vendor/livewire/flux-pro/' exists - if not they need to run `php artisan flux:activate` to enable the 'pro' (pay-for) flux components.

  Testing Checklist:
  - All Livewire functionality works (buttons, filtering, forms)
  - Responsive design works on mobile and desktop
  - Delete buttons are appropriately subtle
  - Forms follow FluxUI patterns
  - Error handling displays properly
  - Layout feels balanced (not too wide or narrow)
  - Make sure all 'plain' blade templates (ie, not livewire components) are updated to use `<x-layouts.app>` rather than the older @extends and @section('content') syntax we used to use

  Approach: Work through templates systematically, test functionality after each conversion, and iterate on spacing/sizing based
   on visual feedback. Follow FluxUI documentation patterns exactly, and prioritize user experience improvements where possible.

