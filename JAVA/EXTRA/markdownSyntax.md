# MARKDOWN SYNTAX
---
## Headings
# H1 Title
## H2 Subtitle
### H3 Section
#### H4 Smaller section

---
## Text styles

**bold text**
*italic text*
~~strikethrough~~
`inline code` (example: `System.out.println("Hello World")`)


---
## Lists
- Bullet list item
- Another item
  - Nested item

1. Numbered list
2. Second item
   1. Sub-item


---
## Links & Images
``` markdown
[Link text](https://example.com)
![Alt text](path/to/image.png) (this is an image which is stored locally)

<!-- Resize with HTML -->
<img src="path/to/image.png" alt="Alt text" width="150"/>
```

---
## Blockquotes & Notes
> This is a blockquote.
> It can span multiple lines.
> > This is a nested blockquote.
> > Nested blockquotes can also be created.
> > > Nested blockquotes can go deeper.

!!! note
    This is a note block.
    It can also span multiple lines.
---
## Horizontal line
``` markdown
---
```
---
## Tables
| Name     | Age | Role   |
|----------|-----|--------|
| Juan     | 21  | Dev    |
| Florencia| 20  | Student|
| Carlos   | 22  | Manager|

---

## Task lists (GitHub flavored)
- [x] Learn Markdown
- [ ] Write notes
- [ ] Share on GitHub

---
## Collapsible sections
<details>
  <summary><b>Click to expand</b></summary>
  Hidden text here.
</details>

---
## Emojis
```markdown
:rocket: :smile: :fire: :sparkles: :books:
```
:rocket: :smile: :fire: :sparkles: :books:

---
## Code blocks
``` java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

``` python
print("Hello, World!")
```

``` markdown
# This is a markdown code block
```

``` plaintext
This is a plaintext code block.
```

---