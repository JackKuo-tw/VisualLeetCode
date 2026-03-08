---
description: Steps for adding a new problem visualization page with consistent styling and project integration.
---

# Workflow: Adding a New Problem Visualization Page

Follow these steps to create a new problem visualization page that matches the "Visual LeetCode" style.

## 1. Project Integration Rules

- **Entrypoint:** Every time you add a new page, you **must** create an entrypoint card in `index.html`. Follow the existing "glass-card" pattern and include relevant tags (Difficulty, Algorithm, Data Structure).
- **Core Assets:** Start with a standard HTML5 template and include **Tailwind CSS** and **highlight.js**.

## 2. Basic HTML Structure

Include these required CDNs and boilerplate:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <!-- Google tag (gtag.js) -->
    <script async src="https://www.googletagmanager.com/gtag/js?id=G-1H6WCCWZS2"></script>
    <script>
        window.dataLayer = window.dataLayer || [];
        function gtag(){dataLayer.push(arguments);}
        gtag('js', new Date());

        gtag('config', 'G-1H6WCCWZS2');
    </script>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Visual LeetCode - [Problem Title]</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Syntax Highlighting (Rule: Must use highlight.js from cdnjs) -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/styles/github-dark.min.css">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/highlight.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/languages/cpp.min.js"></script>
    <style>
        body { background-color: #f8fafc; }
        .code-line { transition: all 0.2s; }
        .code-line.active { background-color: rgba(96, 165, 250, 0.2); border-left: 4px solid #60a5fa !important; }
    </style>
</head>
<body class="text-slate-800 p-0 font-sans">
    <!-- Header (Navigation) -->
    <nav class="border-b border-slate-200 bg-white/80 backdrop-blur-md sticky top-0 z-50">
        <div class="max-w-7xl mx-auto px-6 h-16 flex items-center justify-between">
            <a href="index.html" class="flex items-center gap-2 group">
                <div class="w-8 h-8 rounded-lg bg-blue-600 flex items-center justify-center group-hover:scale-110 transition-transform">
                    <svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5 text-white" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round">
                        <path d="m3 9 9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z" /><polyline points="9 22 9 12 15 12 15 22" />
                    </svg>
                </div>
                <span class="text-xl font-bold tracking-tight text-slate-900">Visual <span class="text-blue-600">LeetCode</span></span>
            </a>
            <div class="flex gap-6">
                <a href="https://github.com/JackKuo-tw/VisualLeetCode" target="_blank" class="text-slate-500 hover:text-slate-900 transition-colors">
                    <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M15 22v-4a4.8 4.8 0 0 0-1-3.5c3 0 6-2 6-5.5.08-1.25-.27-2.48-1-3.5.28-1.15.28-2.35 0-3.5 0 0-1 0-3 1.5-2.64-.5-5.36-.5-8 0C6 2 5 2 5 2c-.3 1.15-.3 2.35 0 3.5A5.403 5.403 0 0 0 4 9c0 3.5 3 5.5 6 5.5-.39.49-.68 1.05-.85 1.65-.17.6-.22 1.23-.15 1.85v4" /><path d="M9 18c-4.51 2-5-3-7-3" /></svg>
                </a>
            </div>
        </div>
    </nav>

    <div class="max-w-6xl mx-auto p-6 md:p-10 space-y-6">
        <!-- Main Content Area -->
    </div>

    <!-- Footer -->
    <footer class="max-w-7xl mx-auto px-6 py-12 border-t border-slate-200 mt-12 flex flex-col md:flex-row justify-between items-center gap-6">
        <p class="text-slate-500 text-sm">&copy; 2026 Visual LeetCode. Created for algorithm enthusiasts.</p>
        <div class="flex gap-8">
            <a href="https://github.com/JackKuo-tw/VisualLeetCode" target="_blank" class="text-slate-400 hover:text-slate-600 transition-colors text-sm font-medium">GitHub</a>
        </div>
    </footer>
</body>
</html>
```

## 3. Highlighting Code Traces

Rule: If a new page has code samples, **must use highlight.js from cdnjs** to highlight it.

To use `highlight.js` with line-by-line tracing:

1.  **Define your code as an array of lines.**
2.  **Initialize the code block:**
    ```javascript
    function initCodeBlock() {
        const container = document.getElementById('code-container');
        codeLines.forEach((lineText, idx) => {
            const div = document.createElement('div');
            div.id = `code-line-${idx}`;
            div.className = 'code-line pl-3 py-0.5 border-l-4 border-transparent whitespace-pre font-mono text-sm flex items-center gap-3';

            const codeSpan = document.createElement('span');
            codeSpan.className = 'language-cpp text-slate-300';
            codeSpan.textContent = lineText;

            div.innerHTML = `<span class="text-xs w-4 text-right text-slate-500">${idx+1}</span>`;
            div.appendChild(codeSpan);
            container.appendChild(div);
            hljs.highlightElement(codeSpan);
        });
    }
    ```
3.  **Active Line Highlighting:**
    Update the `render()` function to add the `active` class to the relevant lines.
    ```javascript
    if (step.lines.includes(i)) lineEl.classList.add('active');
    else lineEl.classList.remove('active');
    ```

## 4. Design Principles

- **Cards:** Use `bg-white`, `p-6`, `rounded-2xl`, `shadow-sm`, `border border-slate-200`.
- **Colors:** Primary blue: `blue-600`. Background: `slate-50`. Text: `slate-800`.
- **Typography:** Standard sans-serif for UI, `font-mono` for code/step indices.
- **Buttons:** Use `transition-colors`, `rounded-lg`, and `hover` states.

## 5. Update Sitemap

- **Sitemap Generation:** Whenever a new page is added, you **must** update `sitemap.xml` to include the URL of the newly created page.
