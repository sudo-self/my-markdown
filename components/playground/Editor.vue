<script lang="ts" setup>
const { rawText, isPreviewActive } = storeToRefs(useStore());

watchEffect(() => {
    if (process.client && rawText.value !== "")
        localStorage.setItem("rawText", JSON.stringify(rawText.value));
});

onMounted(() => {
    // get rawText from localStorage
    const text = localStorage.getItem('rawText');
    if (text && text !== "") rawText.value = JSON.parse(text);
    else rawText.value = `# Welcome to My-Markdown
# H1
## H2
### H3

### Bold

**bold text**

### Italic

*italicized text*

### Blockquote

> blockquote

### Ordered List

1. First item
2. Second item
3. Third item

### Unordered List

- First item
- Second item
- Third item

### Code

`code`

### Horizontal Rule

---

### Link

[Markdown Guide](https://www.markdownguide.org)

### Image

![alt text](https://www.markdownguide.org/assets/images/tux.png)

## Extended Syntax

These elements extend the basic syntax by adding additional features. Not all Markdown applications support these elements.

### Table

| Syntax | Description |
| ----------- | ----------- |
| Header | Title |
| Paragraph | Text |

### Fenced Code Block

```
{
  "firstName": "John",
  "lastName": "Smith",
  "age": 25
}
```

### Footnote

Here's a sentence with a footnote. [^1]

[^1]: This is the footnote.

### Heading ID

### My Great Heading {#custom-id}

### Definition List

term
: definition

### Strikethrough

~~The world is flat.~~

### Task List

- [x] Write the press release
- [ ] Update the website
- [ ] Contact the media

### Emoji

That is so funny! :joy:

(See also [Copying and Pasting Emoji](https://www.markdownguide.org/extended-syntax/#copying-and-pasting-emoji))

### Highlight

I need to highlight these ==very important words==.

### Subscript

H~2~O

### Superscript

\`\`\`
<main>
  <h1>This is a larger code block</h1>
</main>
\`\`\``;
});
</script>

<template>
    <div class="editor d-flex flex-column">
        <div class="header position-sticky d-flex align-items-center weight-500">
            <span>MARKDOWN</span>
            <button @click="isPreviewActive = !isPreviewActive">
                <IconsPreview :is-preview-active="isPreviewActive" />
            </button>
        </div>
        <textarea class="editor__area" v-model="rawText"></textarea>
    </div>
</template>

<style lang="scss" scoped>
.editor {
    overflow: auto;

    .header {
        top: 0;
        justify-content: space-between;

        padding: 1.2rem 1.6rem;
        background-color: var(--deeper-bg-color);
        color: var(--sub-text-color);

        span {
            @include font(1.4rem, 1.6rem);
        }

        button {
            display: none;
            color: var(--sub-text-color);
            width: 1.6rem;
            height: 1.2rem;

            @media (max-width: 768px) {
                display: block;
            }

            svg {
                height: 100;
            }
        }
    }

    &__area {
        flex: 1;
        padding: 0.9rem 1.6rem;
        background-color: var(--bg-color);
        color: var(--header-text-color);
        overflow: auto;
        // reset textarea style
        border: none;
        outline: none;
        resize: none;
        // font
        @include font(1.4rem, 1.6rem);
    }
}
</style>
