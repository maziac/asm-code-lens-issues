# ASM Code Lens (v3.0)
ASM Code Lens is a Visual Studio Code extension that enhances working with assembly source code by providing language-server features such as navigation, symbol analysis, and syntax highlighting.

Version 3.0 introduces explicit assembler selection, which enables more accurate syntax highlighting and behavior tailored to the assembler you actually use, even on a per-workspace basis.

This was a very extensive change. Almost all of the code was rewritten. Despite extensive testing, **please bear with me if you encounter any bugs, and please take advantage of the option to report them**.

# Key Features
- [Syntax highlighting](#syntax-highlighting) for x86 and Z80 assembly
- [Code Lenses](#code-lenses)
- [Outline view](#outline-view)
- [Hover information](#hovering)
- [Open symbol by name](#open-symbol-by-name)
- [Go to Definition](#goto-definition)
- [Rename labels](#rename-label)
- [Code folding](#code-folding)
- [Dead code detection (unreferenced labels)](#find-dead-code)
- Completions
- Markdown code block highlighting (```asm, ```list)
- Built-in [hexadecimal/decimal calculator](#hexadecimal-calculator)

# New in Version 3.0: Assembler Awareness
ASM Code Lens 3.0 lets you explicitly **select which assembler syntax is used**, enabling more precise syntax highlighting and parsing.

Supported Assemblers

x86
- NASM
- MASM
- GAS

Z80
- sjasmplus

[ii](#new-in-version-30-assembler-awareness)
**Global and Per-Workspace Configuration**

You can configure the assembler globally or per workspace/project, making it easy to work with multiple codebases that use different assemblers.

This avoids generic “one-size-fits-all” highlighting and significantly improves readability and correctness of assembler syntax.

You can change it globally or per workspace in the settings:
![](assets/remote/settings-asm-selection.jpg)

For each assembler you can choose which file extensions are used:
![](assets/remote/settings-asm-file-extensions.jpg)


If ASM Code Lens version 3 is started for the first time the assembler id is set globally to x86/nasm (language id: asm-x86-nasm).
If you are using some other assembler change it via:
![](assets/remote/settings-asm-selection.jpg)


# Language Ids
Some background information:
ASM Code Lens now uses separate language IDs:
- asm-x86-nasm
- asm-x86-masm
- asm-x86-gas
- asm-z80-sjasmplus
- asm-z80-sjasmplus-list

This allows each assembler to have its own syntax highlighting rules.
Before that (v2.x), a shared language ID tried to include the keywords of all assemblers in a single grammar, which caused incorrect highlighting in some cases.

Note: The old language IDs (asm-collection and asm-list-file) have been removed and are no longer valid. ASM Code Lens will automatically migrate them when it starts. Do not use the old language IDs anymore.

# Syntax Highlighting
Syntax highlighting depends on the selected assembler (language ID).

ASM files are highlighted as soon as they are opened.

As a special feature, syntax highlighting also works for code blocks in Markdown files.

Just add ```asm-nasm```, ```asm-masm```, ```asm-gas```, or ```asm-sjasmplus``` to your code blocks. You can also use ```asm-z80``` as a synonym for ```asm-sjasmplus```.

Here is an example:
![](assets/remote/md-code-block.jpg)


# Code Lenses
Code lenses are the core feature of this extension and the reason for its name.
A code lens displays the number of references above a label name:
![](assets/remote/code-lense-ref-count.jpg)

Code lenses are a powerful way to quickly see how labels are used and to navigate through the source code:
![](assets/remote/code-lense.gif)

Note: If a label has a reference count of 0, it is not used anywhere else. That means it is either dead code or unused data.

Another way to use code lenses is to right-click a label and choose “Find All References.”
The references are then shown in the sidebar instead of inline.

# Outline View
An outline view of the assembly is shown and can be used for navigation:
![](assets/remote/outline-view.gif)

# Hovering
When you hover over labels, the subroutine description is shown if available:
![](assets/remote/hovering.jpg)

# Open Symbol by Name
Click in the title bar and enter a symbol prefixed with # to navigate quickly:
![](assets/remote/symbol-ny-name.jpg)

# Goto Definition
Right-click a label and select "Go to Definition" to navigate to it:
![](assets/remote/goto-definition.jpg)

# Rename Label
Right-click a label, select "Rename Symbol", and choose a new name to rename it in all files:
![](assets/remote/rename-label.gif)

# Code Folding
![](assets/remote/code-folding.gif)

# Find Dead Code
Right-click an assembler file in the text editor and select 'Find Labels with no Reference'
![](assets/remote/find-labels-with-no-reference.jpg)
to get a list of labels (in the OUTPUT pane) that are not referenced anywhere in the workspace.

This can help you find dead code, because code or data that is not referenced is usually not used, or the label is unnecessary.

# Hexadecimal Calculator
As an extra, you will find a hexadecimal calculator/converter in the sidebar:
![](assets/remote/hexcalculator.gif)
