# Clean Code Front End

Code is for humans. There are a few simple things we can do to write more robust and maintainable code.

## HTML / CSS
- [x] 1. Proper Formatting
- [x] 2. Meaning / Purposeful Markup
- [x] 3. Meaning / Purposeful Comments
- [x] 4. Consistent Naming Convention
- [x] 5. Reduce Specificity
- [x] 6. Avoid Inline Styles
- [x] 7. External Style Sheets
- [X] 8. External JavaScript

### Proper Formatting

We work in a world of partials, this causes the output files to be rendered in unusual ways. However, that does not matter. What does matter is the formatting of the source files. This means, no trailing white space, proper indentation for parent / child elements, and meaningful white space around elements. Each file should be formatted properly for several reasons;

1.  Readability
    - It is way easier to see if closing tags are missing.
2.  Committing Code
    - When committing code, there only things that should be included are the actual lines of code and not
3.  Code Reviews
    - Code reviews are hard enough. Inconsistent formatting, such as trailing white space or misaligned parent / child elements, it can be difficult to see the new code that needs attention versus the bloat code that can be ignored.
4.  Maintainability
    - Code changes over time. Why not leave a proper foundation for our future selves or future developers?

#### Bad

```HTML
<div class="container">
    <nav class="nav">
    <a href="#"><i class="fa fa-home"></i>
        <span>Home</span></a><a href="#"><i class="fa fa-about"></i>
            <span>About</span></a>
            <a href="#"><i class="fa fa-contact"></i>
                <span>Contact</span></a>
    <a href="#"><i class="fa fa-gallery"></i>
        <span>Gallery</span>
    </a>
</nav>
</div>
```

#### Good

```HTML
<div class="container">
    <nav class="nav">
        <a href="#">
            <i class="fa fa-home"></i>
            <span>Home</span>
        </a>
        <a href="#">
            <i class="fa fa-about"></i>
            <span>About</span>
        </a>
        <a href="#">
            <i class="fa fa-contact"></i>
            <span>Contact</span>
        </a>
        <a href="#">
            <i class="fa fa-gallery"></i>
            <span>Gallery</span>
        </a>
    </nav>
</div>
```

### Meaning / Purposeful Markup

There is a trend to nest extra `div`'s for various reasons. This is especially noticeable with front end frame works. While I understand why libraries like Bootstrap need those `div`'s, my concern is with their necessity overall. We should not be afraid of an extra `div` or `span` tag, but make it have meaning.

Use the correct tag for the correct elements. Meaning, if you have a block of text, use a paragraph tag. If you need to click something, use an anchor or button.

#### Bad

```HTML
<div class="news-story">
    <div class="title">Story Title</div>
    <span class="pub-date">2018-01-01</span>
    <div class="content">This is a story all about how my life got flipped turned upside down...</div>
</div>
```

#### Good

```HTML
<article class="news-story">
    <h1 class="title">Story Title</h1>
    <h6 class="pub-date">2018-01-01</h6>
    <p class="content">This is a story all about how my life got flipped turned upside down...</p>
</article>
```

### Meaning / Purposeful Comments

Code should be as self documenting as possible. But, there are reasons one would want to leave a comment. One could be to leave yourself a reminder or note to the next developer. _These should not make it to production so use VERY sparingly_. More useful would be an indication where something ends. A good habit I picked up early in my career was to open and then immediately close it, as well as note what has been closed. HTML has the tendency to get nested pretty deeply, this can cause it to be difficult to be certain what is open and close properly and where.

### Bad

```HTML
<div class="container">
    <header>
        ...
        <nav>
            ...
        </nav>
    </header>
    <main>
        <div class="posts">
            <div class="post">
                ...
            </div>
            <div class="post">
                ...
            </div>
            <div class="post">
                ...
            </div>
        </div>
    </main>
</div>
```

### Good

```HTML
<div class="container">
    <header>
        ...
        <nav>
            ...
        </nav>
    </header>
    <main>
        <div class="posts">
            <div class="post">
                ...
            </div><!-- /post -->
            <div class="post">
                ...
            </div><!-- /post -->
            <div class="post">
                ...
            </div><!-- /post -->
        </div><!-- /posts -->
    </main>
</div><!-- /container -->
```

### Consistent Naming Convention

Every project you work on is a little different. If you are new to the project, take the time to see what the style is and keep things similar. If you are starting a new project, decide what the naming style is going to be and be **consistent**.

#### Bad

```HTML
<div class="container">
    <header class="main-header">
        <nav id="mainNav">
            <a href="#" class="mainNav__item">Home</a>
            <a href="#" class="mainNav__item">About</a>
            <a href="#" class="mainNav__item">Gallery</a>
        </nav>
    </header>
</div>
```

#### Good

```HTML
<div class="container">
    <header class="header">
        <nav class="nav">
            <a href="#" class="nav__item">Home</a>
            <a href="#" class="nav__item">About</a>
            <a href="#" class="nav__item">Gallery</a>
        </nav>
    </header>
</div>
```

### Reduce Specificity

First, lets define Specificity in CSS.

> **Specificity** is the means by which browsers decide which CSS property values are the most relevant to an element and, therefore, will be applied. Specificity is based on the matching rules which are composed of different sorts of [CSS Selectors](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference#Selectors)
> -- Source [Specificity MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity)

There is a cool tool you can use to determine how *specific* selector rule is. [Specificity Calculator](https://specificity.keegan.st/)

Specificity is broken down into 4 categories:

- Inline +1 ( Most specific )
- IDs +1 ( Very specific )
- Classes +1 ( Generally specific )
    - Attributes
    - pseudo-classes [^1]
- Element +1 ( Least specific )
    - pseudo-elements [^1]

> Basically a pseudo-class is a selector that assists in the selection of something that cannot be expressed by a simple selector, for example `:hover`.
> A pseudo-element however allows us to create items that do not normally exist in the document tree, for example `::after`.
>
> -- source [Growing with the Web](http://www.growingwiththeweb.com/2012/08/pseudo-classes-vs-pseudo-elements.html)

The way you calculate the specificity of a rule is to simply add one to each category that rule has. Your outcome will always be a 4 digit number. Let's take a look and some examples :

```HTML
<div class="item">
    <p id="dark">This is text</p>
</div>
```

```CSS
// 0 1 0 1
p#dark {
    background: red;
}

// 0 0 1 1
.item p {
    background: yellow;
}

// 0 1 1 1
body .item #dark {
    background: cyan;
}

// 0 1 1 0
[class="item"] #dark {
    background: pink;
}

// 0 1 0 3
body div p#dark {
    background: blue;
}

// 0 1 0 0
#dark {
    background: green;
}
```

Now that we understand what specificity is, let's look at a couple of examples that are bad and how we can correct them.

#### Bad

```CSS
nav#nav ul li a {}
.userProfile .social-links a {}
article h2.title {}
section.products div.product {}
```

#### Good

```CSS
#nav a {}
.social-links a {}
.title {}
.product {}
```

### Better

```CSS
.nav__item {}
.social-link {}
.title {}
.product {}
```

By utilizing classes with unique meaningful names you gain the ability to easily over write and avoid clashes with the *cascade* portion of CSS.

### Avoid Inline Styles

As we learned about specificity in the previous section, it should go without saying that inline styles should be avoided. At least the hand created inline styles. If you are manipulating things with JavaScript, such as animations, the inline styles that creates is acceptable.

There are some examples where one might be better suited for adding and removing classes in stead of adding an inline style. For example; hiding and showing something. You should opt for manipulating classes. This gives your more control of the adverse side affects caused by specificity.

### External JavaScript

It is best practice to keep all JavaScript functionality in an external file. Preferably with a good naming convention and structure, and included only on the pages it's needed.

If you absolutely need to write inline JavaScript, it should be done for a clear and arguable reason. Other wise, put it in an external file.

## JavaScript

1.  Proper Formatting
2.  Meaningful Variables
3.  Meaningful Function Names
4.  Minimize Global Scope
5.

### Proper Formatting

Your source files should have proper formatting. The final output render is not important, but the source files should be as clean as possible. This means, no trailing white space, proper indentation for parent / child elements, and meaningful white space around elements.

#### Bad

```JavaScript
var baseURL="http://someapi.com",items=20,user_activity=false;
function posts(string){ return baseURL+string+'?query=123'}
```

#### Good

```JavaScript
var baseURL = "http://someapi.com";
var items = 20;
var user_activity = false;

function posts(string){
    return baseURL + string + "?query=123";
}
```

### Meaningful Variables
