# Creating HTML page on local for CICS CMS systems

## Enviroment

To edit/build CICS pages, you need to prepare:

1. SCSS complier ("scss-to-css" plugin on VS code / Koala)
2. Apache Server for hosting HTML
3. Code editor

## Structure

There is 2 parts on this folder:

- Style files
- HTML file

### Style

Style script are writing in SCSS. This is a language able to split huge CSS code into small files/syntax.

_In CSS:_

```css
.abc .def {
  color: black;
}

.abc .def .gfk {
  color: white;
}
```

_In SCSS_

```scss
.abc {
  .def {
    color: black;

    .gfk {
      color: white;
    }
  }
}
```

### HTML

HTML files including 2 files

- `index.html`
  <br>
  This is the main html for the CICS main element such as Menu, Header, Footer. You can not modify those element when you uploaded your work to CMS system.
- `content.html`
  <br>
  This is the place you can work on it. Those content will be load on the index.html. You should copy the code in this file to the editor of CICS CMS system.

## Apache

Apache is for the CORS issue when loading `content.html`.
Once you installed Apache, you can copy this folder into your htdocs.

## Work flow (Editing)

1. Pull the code from git/Copy this folder with all files.
2. Copy `demo folder` and rename as your page name with no space and lowercase.
3. Access to the folder your copied and start your work on content.html
4. Everytime you edit the scss file. Compiler the scss to with resulting a index.css file in /style dir.
   <br>
   For Example in vscode, you can `Ctrl + Shift + P`, then select "`compiler this scss`"

## Work flow (Upload Content)

1. Login to CMS system.
2. Go to "Content Pages"
3. Choose the pages you are going to upload your work
4. Upload `index.css` from your dir to CMS system
5. Insert the following code into the head of `content.html`
   <br>

```html
<script type="text/javascript">
  function loadCSS(filename) {
    var file = document.createElement("link");
    file.setAttribute("rel", "stylesheet");
    file.setAttribute("type", "text/css");
    file.setAttribute("href", filename);
    document.head.appendChild(file);
  }

  //just call a function to load your CSS
  //this path should be relative your HTML location
  //replace this path from "./style/" to "https://www.cicscanada.com/dat/files/"
  loadCSS("https://www.cicscanada.com/dat/files/13121.css");
</script>
```

6. Copy the file link of index.css from the CMS system.
   <br>
   ![copy](./Capture.PNG "Logo Title Text 1")

7. Modify the url of this syntax into the file link you've copy.

```javascript
loadCSS("https://www.cicscanada.com/dat/files/*******.css");
```

8. Copy all the code from `content.html`
9. Click Save
