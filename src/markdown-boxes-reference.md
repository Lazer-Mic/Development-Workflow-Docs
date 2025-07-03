# Most Useful Markdown Box Syntax

## Code Blocks
```
Single backticks for `inline code`
```

````
Triple backticks for code blocks:
```javascript
function example() {
    return "Hello World";
}
```
````

## Blockquotes
```
> This is a blockquote
> It can span multiple lines
> 
> > Nested blockquotes are also possible
```

## Tables (Box-like structure)
```
| Header 1 | Header 2 | Header 3 |
|----------|----------|----------|
| Cell 1   | Cell 2   | Cell 3   |
| Cell 4   | Cell 5   | Cell 6   |
```

## Admonitions (GitHub/GitLab style)
```
> [!NOTE]
> This is a note admonition

> [!WARNING]
> This is a warning admonition

> [!IMPORTANT]
> This is important information

> [!TIP]
> This is a helpful tip

> [!CAUTION]
> This indicates caution
```

## Details/Summary (Collapsible boxes)
```html
<details>
<summary>Click to expand</summary>

This content is hidden by default and can be expanded.

</details>
```

## Horizontal Rules (Dividers)
```
---
or
***
or
___
```

## Fenced Code Blocks with Languages
```
```python
def hello():
    return "Hello World"
```

```bash
echo "Command example"
```

```json
{
  "key": "value"
}
```
```

## ASCII Box Drawing
```
┌─────────────────┐
│   Box Content   │
└─────────────────┘

╔═════════════════╗
║   Double Lines  ║
╚═════════════════╝
```

## Spacing Techniques

### Two Spaces for Line Breaks
```
Line with trailing spaces  
Next line continues

Another line  
And another
```

### Empty Lines for Vertical Spacing
```
Paragraph 1


Paragraph 2 with space above
```

### Indented Code Blocks (4 spaces)
```
    Indented content
        More indented
            Even more indented
```

### Nested Blockquotes
```
> Level 1
> 
> > Level 2
> > 
> > > Level 3
```

### Lists with Indentation
```
- Item 1
  - Sub-item (2 spaces)
    - Sub-sub-item (4 spaces)

1. Numbered
   - Mixed bullet (3 spaces)
     - Deeper (5 spaces)
```