# Web Twig Starter Kit 🛠

**web-twig-starter-kit is a frontend starter kit based on the Google's [web-starter-kit](https://github.com/google/web-starter-kit). It includes a twig intergration for a reusable-code workflow and other tools for cleaner development.**

---

- [Getting started](#1---getting-started)
- [File structure](#2---file-structure)
  - [Html with twig](#21---html-with-twig)
    - [Extend layouts](#211---extend-layouts)
    - [Include html](#212---include-html)
    - [More about Twig](#213---more-about-twig)
  - [Style with Scss](#22---style-with-scss)

## 1 - Getting started
```
git clone https://github.com/pierrecabriere/web-twig-starter-kit.git
cd web-twig-starter-kit
npm install
gulp serve
```
Now open your browser at **http://localhost:3000**, and ...<br/>
**That's it !** gulp is watching your files and you juste have to write some pieces of code to see the magic of BrowserSync !

## 2 - File structure

The structure of this starter kit is pretty simple: all of your code have to be inside the /app folder.<br/>
All of your html pages should be created at the root of the /app directory.<br/>
By default, the structure of your html pages is in the /app/html/extends/base.html file.

### 2.1 - Html with twig

Twig allows to include html and extends layouts from others files.<br/>
So there are two folders in /app/html, where you can create your twig templates :

#### 2.1.1 - Extend layouts

**/app/html/extends** contains your twig layouts.<br/>
There already is the base layout file with a basic html structure. You can create new layouts or extends others layouts.
```html
{% extends "html/extends/base.html" %}

{% block body %}
  <!--
  Here is your page content, that will be included
  in the body block of the extended file
  -->
{% endblock %}
```

The basic html layout (/app/html/extends/base.html) contains three blocks :
- *title*: contains the specific title of the page (concatenate with the default site title)
- *body*: contains the body of the page
- *javascripts*: contains the inclusion of your javascript dependencies (like jQuery)

##### Example
```html
<!-- /app/mypage.html -->
{% extends "html/extends/base.html" %}

{% block body %}
  My Page Content
{% endblock %}

{% block title %}My Page Title - {% enblock %} <!-- Will be concatenate: My Page Title - My Site Title -->
```

#### 2.1.2 - Include html

**/app/html/includes** contains your reusable code.<br/>
Here you can create configurable pieces of code to include in your pages. A good practise is to create "components", like a button or a menu.

##### Example
Create your component with parameters :
```html
<!-- /app/html/includes/button.html -->
<button class="button {{buttonType}}"><span class="overlay"></span>{{ buttonLabel }}</button>
```
Then, you can reuse your components in your pages :
```html
<!-- /app/mypage.html -->
{% extends "html/extends/base.html" %}

{% block body %}
  My Page Content
  {% include "html/includes/button.html"
     with { buttonType: 'button-bold', buttonLabel: 'Click-me !' } %}
{% endblock %}
```

#### 2.1.3 - More about twig

> For more informations about twig, please reffers to the [official documentation](https://twig.symfony.com).

### 2.2 - Style with Scss

Scss is very flexible: you can even write basic CSS if you don't know the Scss syntax. If you don't know what a preprocessor is and you are interested in this technology, you can read the [official scss documentation](https://sass-lang.com/guide).<br/>
**All your style files have to be in the /app/styles/directory**. To be properly compiled and minified, all of your style have to be in the main.scss file. However, for a proper and more readable code, you shuold create files and include them in the main.scss file.<br/>
A good practice is to create a .scss file for all your app/html/includes templates.

#### Example
```scss
// /app/styles/_buttons.scss
.button {
    background-color: white;
    color: blue;
    
    &.button-bold {
        font-weight: bold;
    }
}
```
Then, you have to include the style in the main.scss file
```scss
@include './buttons'
```

## 3 - Compilation

> More documentation to come

# 🚀
