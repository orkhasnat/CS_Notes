The most beautiful dark theme ever.

For further inquiry - [Royal Velvet](https://github.com/caro401/royal-velvet/blob/main/obsidian.css)

---

```css
.theme-dark{
--gradientDegree: 135deg;

--black: #21222c;
--blackSecondary: #414558;
--blackDark: #1d1e26;
--blackXDark: #14141b;
--blackLighter: #2a2c37;

--white: #f8f8f2;
--white-600: rgba(248, 248, 242, 0.6);
--white-400: rgba(248, 248, 242, 0.4);

--pink: #ff80bf;
--pinkSecondary: #ffcce6;
--pink-100: rgba(255, 128, 191, 0.1);
--pink-300: rgba(255, 128, 191, 0.3);
--pink-400: rgba(255, 128, 191, 0.4);

--green: #8aff80;
--greenSecondary: #d0ffcc;
--green-200: rgba(138, 255, 128, 0.2);

--orange: #ffca80;
--orangeSecondary: #ffeacc;
--orange-100: rgba(255, 202, 128, 0.1);

--purple: #9580ff;
--purple-200: rgba(149, 128, 255, 0.2);

--red: #ff9580;
--red-900: rgba(255, 149, 128, 0.9);

--yellow: #ffff80;
--yellow-100: rgba(255, 255, 128, 0.1);
--yellow-700: rgba(255, 255, 128, 0.7);

--cyan: rgb(128, 255, 234);
--cyan-600: rgba(128, 255, 234, 0.6);

--background-modifier-cover: var(--blackXDark); /*Obsidian Title Bar Bg*/
--background-primary: var(--black); /*Note background*/
--background-primary-alt: var(--blackDark); /*Note Title background active*/
--background-secondary: var(--blackDark); /*Sidebar background*/
--background-secondary-alt: var(--blackXDark); /*Sidebar Title background*/

--background-modifier-border: var(--blackDark); /*Border outline of quotes, tables, line breaks*/
--background-modifier-form-field: var(--pink-100);
--background-modifier-form-field-highlighted: var(--pink-300);
--background-modifier-box-shadow: var(--blackLighter);
--background-modifier-success: var(--green-200);
--background-modifier-error: var(--red-900);
--background-modifier-error-rgb: 61, 0, 0;
--background-modifier-error-hover: var(--red);

--text-normal: var(--white); /*Text body of note*/
--text-muted: var(--white-600); /*Text darker for sidebar, toggles, inactive, tags, etc*/
--text-accent: var(--pink); /*Links*/
--text-accent-hover: var(--pinkSecondary); /*Links hover*/
--text-faint: var(--white-600); /*Link brackets color & Gutter Numbers*/
--text-error: var(--red);
--text-error-hover: var(--redSecondary);

--text-highlight-bg: var(--yellow-100); /*Search Matches*/
--text-highlight-bg-active: var(--orange-100); /*Active Search Match (Preview Mode)*/
--text-selection: var(--purple-200); /*Text Selections*/

--interactive-normal: var(--blackDark); /*Button Color*/
--interactive-hover: var(--blackXDark); /*Button Hovered Color*/
--interactive-accent: var(--pink); /*Workspace Note Title Underline*/
--interactive-accent-hover: var(--pinkSecondary); /*Menu Button Hover*/
--interactive-success: var(--green);

--scrollbar-bg: var(--black); /*Scrollbar Gutter Background*/
--scrollbar-thumb-bg: var(--pink-100); /*Scrollbar Color*/
--scrollbar-active-thumb-bg: var(--pink-300); /*Scrollbar Dragged Color*/
--indentation-guide: var(--blackSecondary);
}
```


```css
/*--Headers/Headings--*/

h1,
.cm-header-1 {
  -webkit-text-fill-color: transparent;
  background-clip: text;
  -webkit-background-clip: text;
  background-image: linear-gradient(
    var(--gradientDegree),
    var(--pink) 0,
    var(--orange) 100%
  );
} /*Source Mode*/
h2,
.cm-header-2 {
  -webkit-text-fill-color: transparent;
  background-clip: text;
  -webkit-background-clip: text;
  background-image: linear-gradient(
    var(--gradientDegree),
    var(--orange) 0,
    var(--yellow) 100%
  );
} /*Source Mode*/
h3,
.cm-header-3 {
  -webkit-text-fill-color: transparent;
  background-clip: text;
  -webkit-background-clip: text;
  background-image: linear-gradient(
    var(--gradientDegree),
    var(--yellow) 0,
    var(--green) 100%
  );
} /*Source Mode*/
h4,
.cm-header-4 {
  -webkit-text-fill-color: transparent;
  background-clip: text;
  -webkit-background-clip: text;
  background-image: linear-gradient(
    var(--gradientDegree),
    var(--green) 0,
    var(--cyan) 100%
  );
} /*Source Mode*/
h5,
.cm-header-5 {
  -webkit-text-fill-color: transparent;
  background-clip: text;
  -webkit-background-clip: text;
  background-image: linear-gradient(
    var(--gradientDegree),
    var(--cyan) 0,
    var(--purple) 100%
  );
} /*Source Mode*/
h6,
.cm-header-6 {
  -webkit-text-fill-color: transparent;
  background-clip: text;
  -webkit-background-clip: text;
  background-image: linear-gradient(
    var(--gradientDegree),
    var(--purple) 0,
    var(--pink) 100%
  );
} 
```

```css
input[type="checkbox"]:checked {
  filter: hue-rotate(36deg) brightness(1.5);
}
/*--Blockquotes--*/
blockquote,
.markdown-preview-view blockquote {
  border: 1px solid;
  border-left-width: 4px;
  border-radius: 4px;
  border-color: var(--purple);
  background-color: var(--blackDark);
  padding: 10px 20px;
  margin-inline-start: 30px;
  margin-inline-end: 30px;
}
```