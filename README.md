# Test Addon — README Renderer Smoke Test

This README exercises every markdown feature the addon manager supports. Rename to `README.md` on GitHub, point a test addon at the commit, and verify each section renders correctly in the addon's Description panel.

---

## Headings

# H1 — should be largest
## H2 — slightly smaller
### H3 — smaller still
#### H4
##### H5
###### H6

## Paragraphs and inline formatting

Plain paragraph text. Should flow naturally with normal spacing between paragraphs.

A second paragraph with **bold text**, *italic text*, ***bold italic***, and `inline code` mixed in. The bold/italic colors should pop against the secondary text color.

A third paragraph just to test paragraph spacing — there should be visible space between this and the previous one, but not too much.

## Bullet lists

- First item
- Second item
- Third item with a longer description that should wrap naturally onto the next visible line if the panel is narrow enough to force wrapping
- Nested bullets:
  - Sub-item one
  - Sub-item two
    - Sub-sub-item
- Back to the top level

## Numbered lists

1. Step one
2. Step two
3. Step three
4. Step four with nested:
   1. Sub-step A
   2. Sub-step B
5. Back to top level

## Inline code and code blocks

Use `local x = 5` to declare a local variable. The `print()` function outputs to the chat window.

```lua
local function greet(name)
    print("Hello, " .. name)
end

greet("Tester")
```

```javascript
// JavaScript example
const total = items.reduce((sum, item) => sum + item.price, 0);
console.log(`Total: $${total.toFixed(2)}`);
```

```
Plain code block with no language — should still render in the monospace
container with a subtle background and border.
```

## Blockquotes

> This is a blockquote. It should render with a green left border, slightly muted text, and a subtle green-tinted background.

> A second blockquote — also indented with the left border.
>
> Including a second paragraph inside the same blockquote.

## Horizontal rule

Above the line.

---

Below the line.

## Tables

| Column A | Column B | Column C |
|----------|----------|----------|
| Row 1A   | Row 1B   | Row 1C   |
| Row 2A   | Row 2B   | Row 2C   |
| Row 3A   | Row 3B   | A longer cell to test wrapping inside table cells |

| Aligned | Left | Right |
|---------|:-----|------:|
| One     | A    | 100   |
| Two     | B    | 1000  |

## Links

- External HTTPS link: [GitHub](https://github.com) — click should open in your default browser (via OpenReadmeLink, not in the webview)
- ArcheRage forums (made up): [click me](https://example.com/forum)
- Mailto link: [email the author](mailto:author@example.com) — should open default mail client
- Anchor link: [jump to top](#test-addon--readme-renderer-smoke-test)

## Images

**Absolute HTTPS URL** (loads from placehold.co):

![Placeholder screenshot 600x300](https://placehold.co/600x300/4a9d7c/white?text=Demo+Screenshot+1)

![Smaller placeholder](https://placehold.co/400x150/1a1a1a/5bb890?text=Feature+Preview)

**Relative path** (resolves against the addon's pinned-commit base URL — will 404 unless you actually have a `screenshot.png` next to the README in the source repo, which is expected for this test):

![Relative image — expected to break unless you add one](screenshot.png)

## Stripped raw HTML

The following raw HTML should be **stripped** by the renderer and render as nothing:

<script>alert('xss')</script>
<img src=x onerror="alert('xss')">
<iframe src="https://example.com"></iframe>

(If you see any of those tags render or fire, the sanitiser is broken.)

## Refused URL schemes

The following links should render as plain text (no clickable anchor) because the renderer refuses non-https / non-mailto schemes:

- `javascript:alert(1)` — [should not be clickable](javascript:alert(1))
- `data:` URL — [should not be clickable](data:text/html,<script>alert(1)</script>)
- `file://` link — [should not be clickable](file:///etc/passwd)

## Mixed real-world content

ArcheRage's `Auto Role Setter` addon is a small quality-of-life tool. Here's what makes it tick:

1. **Detects your current zone** on world enter
2. **Looks up your saved role config** for that zone
3. **Switches automatically** without nagging you

Configuration example:

```yaml
zones:
  Auroria:
    role: PvP
    notify: true
  Diamond Shores:
    role: PvE
    notify: false
```

> ⚠️ **Note:** the addon will refuse to auto-switch during combat. This is intentional — you can override with `/autorole force` if you really mean it.

For bug reports, drop a message in our [Discord](https://discord.com) or open an issue on the [GitHub repo](https://github.com).

---

*If you see this entire document render with proper styling, hyperlinks, images, code blocks, blockquotes, tables, and no security warnings — the README renderer is working as designed.*
