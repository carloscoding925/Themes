# Theme Schema Reference

A guide to every property in a Zed theme JSON file: what it controls and where in the editor you can see the color applied.

Schema URL: `https://zed.dev/schema/themes/v0.2.0.json`

## How to find a property's effect quickly

1. **Live reload.** Drop the theme into `~/.config/zed/themes/` (or symlink it). Zed watches that folder, so saving the file reapplies it within ~1 second.
2. **Toggle to isolate.** When you can't tell where a color is showing, set the key to an obvious color like `#ff00ff` (magenta) temporarily and save. The garish color will jump out wherever it's drawn.
3. **Command palette.** `cmd+shift+p` then search for "theme" to switch between your theme and a reference (e.g. Catppuccin Mocha) to compare a single region.
4. **Open multiple panes.** Many keys only show on specific UI surfaces (terminal, file tree, AI panel, diagnostics popup, find/replace). Open each panel to exercise its colors.

## Top-level structure

| Key | Controls |
|---|---|
| `$schema` | URL of the JSON schema version. Enables editor autocomplete/validation. |
| `name` | Theme **family** name shown in extension lists. |
| `author` | Author string shown in the theme picker. |
| `themes[]` | Array of individual themes in this family (e.g. one light + one dark variant). |

## Per-theme fields

| Key | Controls |
|---|---|
| `name` | The name shown in the theme picker (`cmd+k cmd+t`). |
| `appearance` | `"dark"` or `"light"`. Affects which theme is auto-selected when "match system" mode is on, and which fallbacks Zed uses. |
| `style` | Object containing every visual property below. |

---

## Global accents

| Key | Controls | Where to look |
|---|---|---|
| `accents[]` | Array of rotating accent colors used by features that need a sequence: rainbow indent guides, bracket pair colorization, multiplayer cursors as a fallback. | Enable `"indent_guides": { "coloring": "indent_aware" }` in settings to see all of them in a nested code file. |
| `background.appearance` | `"opaque"`, `"blurred"`, or `"transparent"`. Controls the window's overall transparency mode. | The window itself — toggle and observe whether desktop shows through. |

## Multiplayer cursors

| Key | Controls | Where to look |
|---|---|---|
| `players[]` | Array of `{ cursor, background, selection }` color triplets. Each collaborator gets the next available slot. Slot 0 is also your own cursor color. | Your own caret blinks in `players[0].cursor`. Collaborator caret/selection visible during a Zed call. |

---

## Window chrome (the frame around the editor)

| Key | Controls | Where to look |
|---|---|---|
| `background` | The fill behind the whole app — visible through gaps and rounded corners. | Reduce window size and look at the outer edge / corners. |
| `title_bar.background` | The very top strip of the window with traffic-light buttons. | Top of the Zed window when it has focus. |
| `title_bar.inactive_background` | Title bar fill when the window is unfocused. | Click another app — title bar dims to this color. |
| `toolbar.background` | The horizontal strip directly below the title bar (breadcrumbs, action buttons). | Open a file — the breadcrumb row above the editor. |
| `status_bar.background` | The bottom strip showing diagnostics count, branch, cursor position. | Very bottom of the Zed window. |
| `tab_bar.background` | The strip the file tabs sit in (excluding the tabs themselves). | Open multiple files — the bar behind the tabs. |
| `tab.active_background` | Fill of the **currently focused** file tab. | The tab matching the file you're editing. |
| `tab.inactive_background` | Fill of all other open tabs. | Any open-but-not-focused tab. |

## Borders

| Key | Controls | Where to look |
|---|---|---|
| `border` | Default 1px borders between UI regions (panel edges, tab dividers). | Edge between file tree and editor. |
| `border.variant` | A second border tone for nested separators. | Subtle dividers inside the assistant panel or settings UI. |
| `border.focused` | Highlight color around a focused element. | Tab through inputs / click on the search field in find/replace. |
| `border.selected` | Border around a selected list item (e.g. project picker). | `cmd+p` and arrow-key down the list. |
| `border.transparent` | Placeholder/no-op border slot. | Rarely visible — used where Zed wants to reserve layout space without drawing. |
| `border.disabled` | Border on disabled inputs/buttons. | Disabled buttons in settings or modal dialogs. |

## Surfaces & elements (clickable things)

| Key | Controls | Where to look |
|---|---|---|
| `surface.background` | Modal/popover fill (e.g. autocomplete dropdown body). | Trigger code completion and look at the popover. |
| `elevated_surface.background` | Floating-above-surface fill — tooltips, context menus, command palette. | `cmd+shift+p`. |
| `element.background` | Default fill of buttons / pills / interactive list items. | Buttons in the AI assistant panel. |
| `element.hover` | Element fill on mouse-over. | Hover over any button. |
| `element.active` | Element fill while being clicked (mouse-down). | Click and hold a button. |
| `element.selected` | Element fill when toggled on / currently selected. | Selected file in the project file tree. |
| `element.disabled` | Element fill when disabled. | A grayed-out toolbar button. |
| `ghost_element.background` | Transparent variant — used for elements that should only show on hover/active. Usually `#00000000`. | Generally invisible by design. |
| `ghost_element.hover` | Fill that appears when hovering a "ghost" element. | Hover over a sidebar icon. |
| `ghost_element.active` | Same on mouse-down. | Click and hold a sidebar icon. |
| `ghost_element.selected` | Selected state for ghost elements. | The currently-active left sidebar icon (file tree / search / git etc). |
| `ghost_element.disabled` | Disabled ghost element. | Rarely shown. |
| `drop_target.background` | Highlight rectangle when dragging a file/tab to a new pane location. | Drag a tab over another pane. |

## Text & icons

| Key | Controls | Where to look |
|---|---|---|
| `text` | Default UI text color (NOT editor body text — that's `editor.foreground`). | Labels in the status bar, side panel headings. |
| `text.muted` | Secondary/subtle UI labels. | "No results" messages, hint labels. |
| `text.placeholder` | Placeholder text inside empty text inputs. | Empty search field. |
| `text.disabled` | Text in disabled controls. | Disabled menu items. |
| `text.accent` | UI text that should pop (links in modals, highlights). | "Sign in" or other call-to-action text. |
| `icon` | Default icon stroke/fill. | Sidebar icons, status bar icons. |
| `icon.muted` | Secondary/inactive icons. | Inactive sidebar icons. |
| `icon.placeholder` | Icons inside empty states. | Empty file tree placeholder icon. |
| `icon.disabled` | Disabled icon fill. | Disabled action buttons. |
| `icon.accent` | Highlighted icon (e.g. unread indicator). | Notification dot icons. |

## Panels & panes

| Key | Controls | Where to look |
|---|---|---|
| `panel.background` | Fill of left/right/bottom panels (file tree, terminal, AI, chat, git). | Open the file tree (`cmd+shift+e`). |
| `panel.focused_border` | Border around a panel when it has focus. | Click into the terminal panel — its outline. |
| `panel.indent_guide` | Vertical guide lines in the **project file tree** (not the editor). | Expanded nested folder in the file tree. |
| `panel.indent_guide_active` | Indent guide along the currently selected file's path. | Select a deeply-nested file. |
| `panel.indent_guide_hover` | Indent guide along the hovered file's path. | Mouse-hover a file in the tree. |
| `panel.overlay_background` | Background for overlay panels (e.g. quick action search). | The "find" overlay shown above the editor. |
| `pane.focused_border` | Outline of the editor pane that has keyboard focus. | Split editor (`cmd+k cmd+right`), click between panes. |
| `pane_group.border` | Divider between split editor panes. | The vertical line between two open editors. |

## Editor body

| Key | Controls | Where to look |
|---|---|---|
| `editor.background` | The main editing canvas behind your code. | Any open file. |
| `editor.foreground` | Default code text color (used when no syntax token matches). | Plain text or unrecognized tokens. |
| `editor.gutter.background` | The vertical strip on the left showing line numbers. | Left margin of any file. |
| `editor.subheader.background` | Background for editor section dividers (e.g. multi-buffer file headers in search results). | Run a project-wide find (`cmd+shift+f`) and look at the file headers in results. |
| `editor.active_line.background` | Highlight of the line the cursor is on. | Move your cursor — the row that follows it. |
| `editor.highlighted_line.background` | Used for "go to line" / temporary line highlights. | `cmd+g` to jump to a line — the brief flash. |
| `editor.line_number` | Color of inactive line numbers in the gutter. | All line numbers except the cursor's row. |
| `editor.active_line_number` | Color of the line number on the cursor's row. | Line number of the row you're editing. |
| `editor.invisible` | Whitespace markers (when `show_whitespaces` is enabled). | Enable `"show_whitespaces": "all"` in settings. |
| `editor.wrap_guide` | The vertical ruler at the wrap column (e.g. 80 chars). | Set `"wrap_guides": [80]` in settings. |
| `editor.active_wrap_guide` | The wrap guide on the cursor's line (if highlighted differently). | Move cursor onto/off the wrap column. |
| `editor.indent_guide` | Vertical lines showing indentation levels **inside code**. | Any indented code (Python, YAML, nested JS). |
| `editor.indent_guide_active` | Indent guide for the block the cursor is currently in. | Place cursor inside a nested block. |
| `editor.document_highlight.read_background` | Highlight of other occurrences of the symbol your cursor is on (read references). | Click on a variable — other usages get this background. |
| `editor.document_highlight.write_background` | Same, but for **write** references (assignments to the symbol). | Click on a variable that's reassigned elsewhere. |
| `editor.document_highlight.bracket_background` | Highlight of the matching bracket/brace/paren. | Click next to `}` — the matching `{` gets this color. |
| `editor.debugger_active_line.background` | Row highlight for the line the debugger is paused on. | Hit a breakpoint while debugging. |

## Search

| Key | Controls | Where to look |
|---|---|---|
| `search.match_background` | Highlight of all matches in the current find. | `cmd+f` and type a query. |
| `search.active_match_background` | The currently-selected match (different from the others). | After `cmd+f`, the match the cursor is on. |

## Scrollbar

| Key | Controls | Where to look |
|---|---|---|
| `scrollbar.thumb.background` | The draggable scrollbar handle on the right edge. | Long file — the thumb on the right. |
| `scrollbar.thumb.hover_background` | Thumb color on mouse-over. | Hover the scrollbar thumb. |
| `scrollbar.thumb.active_background` | Thumb color while dragging. | Click and drag the thumb. |
| `scrollbar.thumb.border` | Outline of the thumb. | Edges of the scrollbar thumb. |
| `scrollbar.track.background` | The track the thumb slides along. | The strip behind the scrollbar thumb. |
| `scrollbar.track.border` | Outline of the track. | Left edge of the scrollbar track. |

## Minimap

| Key | Controls | Where to look |
|---|---|---|
| `minimap.thumb.background` | The visible-viewport indicator in the minimap. | Enable `"minimap": { "show": "always" }` in settings. |
| `minimap.thumb.hover_background` | Same on mouse-over. | Hover the minimap viewport box. |
| `minimap.thumb.active_background` | Same while dragging. | Click-drag the minimap. |
| `minimap.thumb.border` | Outline of the viewport indicator. | Edge of the minimap viewport box. |

## Terminal

| Key | Controls | Where to look |
|---|---|---|
| `terminal.background` | Terminal panel background. | `ctrl+\`` to open the terminal. |
| `terminal.foreground` | Default terminal text color. | Any plain output. |
| `terminal.bright_foreground` | Default for "bright" text mode. | Programs that print bold/bright text. |
| `terminal.dim_foreground` | Default for "dim" text mode. | Output styled with the dim ANSI attribute. |
| `terminal.ansi.background` | Override for the terminal background, distinct from `terminal.background` (rarely differs). | The terminal canvas. |
| `terminal.ansi.{black,red,green,yellow,blue,magenta,cyan,white}` | The standard 8 ANSI colors. | Run `ls --color` or any colored CLI tool. |
| `terminal.ansi.bright_{...}` | Same 8 colors in their "bright" variants (codes 90–97). | Programs that use bold colors (e.g. `git status`). |
| `terminal.ansi.dim_{...}` | Same 8 colors in their "dim" variants. | Programs that apply the dim attribute. |

## Links

| Key | Controls | Where to look |
|---|---|---|
| `link_text.hover` | Color of UI links on hover (e.g. file paths in diagnostics). | Hover over a URL in the assistant panel or a file path in a diagnostic. |

## Diagnostics & status (used by LSP + UI feedback)

Each of these has three variants: bare color (text), `.background` (highlight fill), `.border` (underline / outline).

| Key | Controls | Where to look |
|---|---|---|
| `success` | Success states (test passed, action completed). | Run tests — the green-pass indicator. |
| `warning` | Warning diagnostics from language servers. | Code with an LSP warning — wavy underline + gutter dot. |
| `error` | Error diagnostics. | Code with a syntax/type error. |
| `info` | Informational diagnostics. | LSP hover info, sometimes lint suggestions. |
| `hint` | Hint diagnostics (weakest level). | Subtle LSP hints (e.g. unused-import). |
| `predictive` | Inline AI/Copilot prediction ghost text. | Type code with Copilot or Zed's prediction on — the gray suggestion. |
| `unreachable` | Code marked as unreachable by analysis. | Code after a `return`/`panic!()` that's flagged unreachable. |

## Diff / version control (in-editor diff view)

Each has bare color, `.background`, `.border`.

| Key | Controls | Where to look |
|---|---|---|
| `created` | Added lines/files in diffs. | Stage view in git panel — new files. |
| `deleted` | Removed lines/files. | Diff view of a delete. |
| `modified` | Modified lines/files. | Diff view of an edit. |
| `renamed` | Renamed files. | Rename in `git status`. |
| `conflict` | Merge conflict markers/lines. | Open a file with `<<<<<<<` conflict markers. |
| `hidden` | Hidden items in lists. | Hidden files in the file tree (with `"file_scan_exclusions"`). |
| `ignored` | Gitignored items. | `.gitignore`-matched files in the tree (greyed out). |

## Version control (gutter + UI)

These are the **current** keys Zed uses for git status — the older `created/deleted/modified` keys above are kept for compatibility but the version_control namespace is what newer Zed features check.

| Key | Controls | Where to look |
|---|---|---|
| `version_control.added` | Added-line markers in the editor gutter. | Add a new line and save — gutter mark. |
| `version_control.deleted` | Deleted-line gutter markers. | Delete a line. |
| `version_control.modified` | Modified-line gutter markers. | Edit an existing line. |
| `version_control.renamed` | Renamed-file indicators. | File tree icon for a renamed file. |
| `version_control.conflict` | Conflict indicators in the git panel. | File with merge conflicts in the git panel. |
| `version_control.conflict_marker.ours` | Background of the `<<<<<<< HEAD` block in a conflict. | Open a conflicted file. |
| `version_control.conflict_marker.theirs` | Background of the `>>>>>>> branch` block in a conflict. | Open a conflicted file. |
| `version_control.ignored` | Color for gitignored files in lists/tree. | `.gitignore`-matched files. |

## Debugger

| Key | Controls | Where to look |
|---|---|---|
| `debugger.accent` | The accent color used across the debugger UI (breakpoint dots, debug panel highlights). | Set a breakpoint — the dot in the gutter. |

(See also `editor.debugger_active_line.background` above.)

## Vim mode indicators

These only show if vim mode is enabled (`"vim_mode": true`). The status bar shows a colored mode badge at the bottom-right.

| Key | Controls | Where to look |
|---|---|---|
| `vim.mode.text` | Default text color of the mode badge. | Status bar mode pill. |
| `vim.normal.foreground` / `.background` | NORMAL mode pill. | Press `esc` in a file. |
| `vim.insert.foreground` / `.background` | INSERT mode pill. | Press `i`. |
| `vim.visual.foreground` / `.background` | VISUAL mode pill. | Press `v`. |
| `vim.visual_line.foreground` / `.background` | VISUAL-LINE mode pill. | Press `V`. |
| `vim.visual_block.foreground` / `.background` | VISUAL-BLOCK mode pill. | Press `ctrl+v`. |
| `vim.replace.foreground` / `.background` | REPLACE mode pill. | Press `R`. |
| `vim.helix_normal.foreground` / `.background` | Helix-style NORMAL mode (when using Helix bindings). | Switch to helix mode binding scheme. |
| `vim.helix_select.foreground` / `.background` | Helix SELECT mode pill. | Helix bindings. |

---

## Syntax tokens (`style.syntax`)

Each entry is `{ "color": "#...", "font_style": "italic"|"normal"|null, "font_weight": 100..900|null }`.

Important: Zed does **not** automatically inherit from parent tokens. `keyword.return` will NOT use `keyword`'s color unless explicitly set. Always define sub-tokens you want themed.

To identify which token a piece of code uses: open the command palette and run `editor: copy highlight json` or hover with a recent Zed build that shows token names in the debug hover.

### Variables

| Token | Matches | Example |
|---|---|---|
| `variable` | Local variables, generic identifiers. | `let **x** = 1;` |
| `variable.builtin` | Built-in language variables. | `**self**`, `**this**`, `**super**` |
| `variable.parameter` | Function parameters. | `fn foo(**x**: i32)` |
| `variable.member` | Object/struct member access. | `user.**name**` |
| `variable.special` | Specially-emphasized variables. | Magic globals like `__name__` |
| `parameter` | Alias for `variable.parameter` (some grammars use this). | Same as above. |
| `field` | Alias for `variable.member`. | Same as above. |

### Constants

| Token | Matches | Example |
|---|---|---|
| `constant` | User-defined constants. | `const **MAX**: u32 = 10;` |
| `constant.builtin` | Built-in constants. | `**True**`, `**None**`, `**nil**` |
| `constant.macro` | Macro constants. | Rust `**println!**` style identifiers in some grammars. |

### Functions

| Token | Matches | Example |
|---|---|---|
| `function` | Function name at definition. | `fn **foo**() {}` |
| `function.builtin` | Built-in/standard library functions. | `**print**(...)`, `**len**(...)` |
| `function.call` | Function name at call site. | `**foo**()` |
| `function.method` | Method definition. | `def **bar**(self):` |
| `function.method.call` | Method invocation. | `obj.**bar**()` |
| `function.macro` | Macro invocation. | Rust `**println!**(...)` |
| `function.decorator` | Decorator/annotation. | Python `**@dataclass**` |
| `function.special.definition` | Special definition forms (varies by grammar). | Reserved by some grammars. |
| `constructor` | Constructor / class instantiation. | `**Point**(1, 2)`, `new **User**()` |

### Types

| Token | Matches | Example |
|---|---|---|
| `type` | User-defined types. | `struct **User**`, `class **Foo**` |
| `type.builtin` | Built-in primitive types. | `**i32**`, `**string**`, `**bool**` |
| `type.definition` | Type at its definition site. | `type **Alias** = ...` |
| `type.interface` | Interface / trait types. | `interface **Reader**` |
| `type.super` | Parent/super type. | `class Foo(**Bar**):` |
| `type.class.definition` | Class definition name (some grammars). | `class **Foo**` |
| `enum` | Enum names. | `enum **Color**` |
| `variant` | Enum variants. | `Color::**Red**` |

### Keywords

All `keyword.*` sub-variants exist as separate tokens — set each one if you want any of them themed.

| Token | Matches | Example |
|---|---|---|
| `keyword` | Generic keywords (catch-all). | `**let**`, `**const**` |
| `keyword.function` | Function-definition keywords. | `**fn**`, `**def**` |
| `keyword.modifier` | Visibility/modifier keywords. | `**pub**`, `**static**`, `**async**` |
| `keyword.type` | Type-introduction keywords. | `**struct**`, `**class**`, `**enum**` |
| `keyword.return` | Return keyword. | `**return** x;` |
| `keyword.import` | Import/use keywords. | `**import**`, `**use**`, `**from**` |
| `keyword.export` | Export keyword. | `**export**` |
| `keyword.conditional` | If/else/match. | `**if**`, `**else**`, `**match**` |
| `keyword.conditional.ternary` | Ternary operator. | `?` in `a ? b : c` (some grammars). |
| `keyword.repeat` | Loop keywords. | `**for**`, `**while**`, `**loop**` |
| `keyword.exception` | Try/catch/throw. | `**try**`, `**catch**`, `**raise**` |
| `keyword.operator` | Word operators. | `**and**`, `**or**`, `**not**`, `**in**` |
| `keyword.coroutine` | async/await. | `**async**`, `**await**` |
| `keyword.debug` | Debug keywords. | `**debugger**` (JS), `**dbg!**` (Rust). |
| `keyword.directive` | Preprocessor/directive keywords. | `**#define**`, `**#include**` |
| `keyword.directive.define` | The defining directive specifically. | `**#define** FOO 1` |

### Strings & characters

| Token | Matches | Example |
|---|---|---|
| `string` | String literals. | `"**hello**"` |
| `string.escape` | Escape sequences inside strings. | `"\\**n**"`, `"\\**t**"` |
| `string.regex` / `string.regexp` | Regex literals. | `/**foo+**/` |
| `string.special` | Specially-marked strings. | Format placeholders in some grammars. |
| `string.special.path` | Path-like strings. | `"./**src**/lib.rs"` |
| `string.special.symbol` | Symbol-like strings. | Ruby `**:symbol**` |
| `string.special.url` | URLs inside strings. | `"**https://...**"` |
| `string.documentation` / `string.doc` | Doc strings. | Python `"""**docstring**"""` |
| `character` | Character literals. | Rust `'**a**'` |
| `character.special` | Character escapes. | `'\\**n**'` |

### Numbers

| Token | Matches | Example |
|---|---|---|
| `number` | Integer literals. | `**42**` |
| `number.float` | Float literals. | `**3.14**` |
| `float` | Alias for `number.float` (some grammars). | Same. |
| `boolean` | Boolean literals. | `**true**`, `**false**` |

### Comments

| Token | Matches | Example |
|---|---|---|
| `comment` | Regular comments. | `// **hello**` |
| `comment.doc` / `comment.documentation` | Doc comments. | `/// **public API**`, `/** ... */` |
| `comment.info` | INFO-tagged comments. | `// **INFO:** something` |
| `comment.hint` | HINT-tagged comments. | `// **HINT:** ...` |
| `comment.note` | NOTE-tagged comments. | `// **NOTE:** ...` |
| `comment.todo` | TODO comments. | `// **TODO:** fix this` |
| `comment.warning` / `comment.warn` | WARNING comments. | `// **WARNING:** ...` |
| `comment.error` | ERROR-tagged comments. | `// **ERROR:** ...` |

### Punctuation & operators

| Token | Matches | Example |
|---|---|---|
| `operator` | Symbolic operators. | `**+**`, `**==**`, `**=>**` |
| `punctuation` | Generic punctuation. | catch-all for `,`, `;`, etc. |
| `punctuation.bracket` | Brackets/braces/parens. | `**( )**`, `**[ ]**`, `**{ }**` |
| `punctuation.delimiter` | Delimiters. | `**,**`, `**;**`, `**:**` |
| `punctuation.list_marker` | Markdown list bullets. | `**-** item`, `**1.** item` |
| `punctuation.special` | Specially-marked punctuation. | `**$**` in template strings, `**#**` in directives. |
| `punctuation.special.symbol` | Symbol-prefix punctuation. | `**:**` in Ruby symbols. |

### Tags & attributes (HTML/JSX/XML)

| Token | Matches | Example |
|---|---|---|
| `tag` | Element tag names. | `<**div**>` |
| `tag.attribute` | Attribute names. | `<div **class**="x">` |
| `tag.delimiter` | `<` `>` `/`. | `**<**div**>**` |
| `tag.doctype` | Doctype declarations. | `**<!DOCTYPE html>**` |
| `attribute` | Generic attribute / annotation. | Rust `**#[derive(...)]**`, decorators in some grammars. |
| `property` | Object property names. | `{ **name**: "x" }`, CSS `**color**: red` |

### Diff blocks

| Token | Matches | Example |
|---|---|---|
| `diff.plus` | `+` added lines in diff views. | `+ **new line**` |
| `diff.minus` | `-` removed lines. | `- **old line**` |

### Markdown / prose

| Token | Matches | Example |
|---|---|---|
| `title` | Markdown headings. | `# **Heading**` |
| `emphasis` | Italic text. | `*italic*` |
| `emphasis.strong` | Bold text. | `**bold**` |
| `text` | Plain prose text. | Paragraph body in `.md`. |
| `text.literal` | Inline code spans. | `` `code` `` in markdown. |
| `link_text` | The visible part of a markdown link. | `[**click here**](url)` |
| `link_uri` | The URL part. | `[click](**https://...**)` |
| `embedded` | Embedded language inside another. | JS inside HTML `<script>`. |

### Misc / grammar-specific

| Token | Matches | Notes |
|---|---|---|
| `module` / `namespace` | Module/namespace names. | `**std**::collections`, Python `**os**.path` |
| `label` | Loop/goto labels. | Rust `**'outer**:` |
| `concept` | C++ concepts and similar. | `concept **Iterable**` |
| `symbol` | Symbol literals (catch-all). | `**:foo**` in Ruby. |
| `parent` | "Parent" reference in some grammars. | Rarely used. |
| `primary` | Primary expression highlight. | Grammar-specific. |
| `predoc` / `preproc` | Preprocessor/predoc tokens. | C `**#pragma**`. |
| `predictive` | AI prediction ghost text inside syntax (separate from top-level `predictive`). | Inline completion preview. |
| `hint` | Inline hint tokens (separate from diagnostic `hint`). | Inlay hints for type/parameter names. |

---

## Tips for filling in colors

- **Backgrounds get darker as you go deeper.** Order: `background` (outermost frame) → `surface.background` → `editor.background` → `elevated_surface.background` (popups *above* the editor, sometimes lighter). Keeping a clear stack makes the UI feel layered.
- **Borders should be slightly lighter than the surface they sit on.** Otherwise they're invisible.
- **`syntax` tokens with no `font_style`/`font_weight` set should omit those keys** — Zed treats omitted as "inherit default". Setting `"font_style": null` works but compact is preferred.
- **Test against a polyglot file.** Open a Rust file (lifetimes, macros), a Python file (decorators, f-strings), a TypeScript file (JSX, generics), and a Markdown file. Each exercises a different swath of tokens.
- **Use the reference theme side-by-side.** Switch between Coffeebeans and Catppuccin Mocha (`cmd+k cmd+t`) on the same file to spot tokens you forgot to style.
