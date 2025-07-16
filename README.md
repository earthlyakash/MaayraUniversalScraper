# 🖼️ Universal Web Image Scraper – Step-Based UI Guide

This tool lets you scrape images from any website using a **dynamic step-based UI**.

## 📌 Key Features

- Build scraping logic by adding steps like `class`, `id`, `tag`, `click`, etc.
- Automatically creates folders from attributes like `id`, `data-asin`, etc.
- Click-through support to scrape deeper pages.
- Auto-extracts image links from `src`, `style`, `data-src`, `data-a-dynamic-image`, and more.

---

## 📋 Step Types You Can Use

| Step Type        | Example                  | Description                                                                 |
|------------------|--------------------------|-----------------------------------------------------------------------------|
| `.class`         | `.class:product-card`    | Selects elements by class name                                              |
| `#id`            | `#id:main-img`           | Selects a single element by ID                                              |
| `tag`            | `tag:img`                | Selects all elements with this tag                                          |
| `@attribute`     | `@attribute:src`         | Reads image URLs from attributes like `src`, `style`, etc.                  |
| `@folder`        | `@folder:data-asin`      | Extracts this attribute's value to use as folder name for saving images     |
| `click`          | `click`                  | Clicks the element (to open product or gallery pages)                       |

---

## 🧠 How the UI Works

### 🔹 Step Builder UI (Left Side)
- You define your scraping logic step-by-step.
- For each step, you select a **type** (e.g., `.class`, `tag`, `click`) and a **value**.

### 🔹 Example Structure

To scrape product search results, click the product, and download images:

```plaintext
.class:s-result-item
  @folder:data-asin
  tag:img
    click
      class:imageThumbnail
        click
      class:image
        tag:img
```

### 🧠 What This Does:

1. Find each product item by class `s-result-item`
2. Use `data-asin` to create folder names (like `B076CHQJZN`)
3. Click the product image (opens the full product page)
4. Click all image thumbnails on the product page
5. From each thumbnail click, grab the updated large image

---

## 📷 Supported Image Sources

Scraper will extract images from any of the following (automatically):
- `src`
- `data-src`
- `style` (background-image)
- `data-a-dynamic-image`
- `srcset` (highest quality version)

---

## ✨ Use Case:Product Page

**HTML Snippet:**
```html
<img src="...w-512.jpg"
     srcset="...w-512 1x, ...w-1080 2x, ...w-1536 3x" />
```

### Step Tree:
```plaintext
tag:img
```

This will scrape **all versions** of the image using both `src` and `srcset`.

---

## 🧠 Advanced Tips

- You can **nest steps** under any tag or class to go deeper.
- Use `click` to navigate through modals or new product views.
- `@folder:<attr>` is required if you want to create a separate folder per item.

---

## ✅ Final Folder Output Example

```
output/
├── B076CHQJZN/
│   ├── image_1.jpg
│   └── image_2.jpg
├── B09FDSXL38/
│   └── image_1.jpg
```


## 🏷️ Common HTML Tag Types (for `tag:<value>`)

| Tag       | Description                          |
|-----------|--------------------------------------|
| `div`     | Generic container                    |
| `img`     | Image element                        |
| `a`       | Anchor / Link                        |
| `span`    | Inline container                     |
| `li`      | List item                            |
| `ul`/`ol` | Unordered / Ordered list             |
| `button`  | Button                               |
| `input`   | Input field                          |
| `h1`-`h6` | Headings                             |
| `p`       | Paragraph                            |
| `section` | Document section                     |
| `article` | Blog/article container               |
| `form`    | Form wrapper                         |

---

## 🧩 Common HTML Attributes (for `@attribute:<value>` or `@folder:<value>`)

| Attribute              | Description                                          |
|------------------------|------------------------------------------------------|
| `src`                  | Image source (used in `<img>`)                       |
| `srcset`               | Set of high-res images                              |
| `style`                | Inline CSS (can include background-image URLs)       |
| `data-*`               | Custom data attributes (e.g., `data-asin`, `data-id`)|
| `id`                   | Unique ID of an element                              |
| `class`                | CSS class(es) for styling / targeting                |
| `alt`                  | Alternative text for images                          |
| `title`                | Tooltip text shown on hover                          |
| `href`                 | URL for `<a>` links                                  |
| `data-a-dynamic-image`| Amazon-style JSON image map                          |

---

## 🔁 Special UI Steps

| Step Type     | Syntax Example           | Description                                                              |
|---------------|--------------------------|--------------------------------------------------------------------------|
| `.class`      | `.class:product-card`    | Selects all elements with this class                                    |
| `#id`         | `#id:main-container`     | Selects element by its ID                                               |
| `tag`         | `tag:img`                | Targets HTML tag like img, div, etc.                                    |
| `@attribute`  | `@attribute:src`         | Grabs value from that attribute (for image URLs or metadata)            |
| `@folder`     | `@folder:data-asin`      | Creates folders named after that attribute value                        |
| `click`       | `click`                  | Clicks the matched element (triggers opening or changing content)       |

---

## ⚙️ Real Use Case Examples

### Product Page
```plaintext
.class:s-result-item
  @folder:data-asin
  tag:img
    click
      class:imageThumbnail
        click
      class:image
        tag:img
```

---

## 💡 Tip: Use Browser DevTools

Use right-click → Inspect Element to find:
- Tag name (e.g., `<img>`)
- Class name
- Attributes like `data-id`, `src`, etc.

Use those values directly in the UI step inputs.

---

---

## 🚀 Ready to Use
- This project runs as a PyQt5 GUI.
- Selenium Chrome driver is used to load dynamic websites.

---
## Free Licence
## 🧑‍💻 Created by: [Akash Kumar]

---
