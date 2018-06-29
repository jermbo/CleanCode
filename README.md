# Clean Code Front End

Code is for humans. There are a few simple things we can do to write more robust and maintainable code.

## HTML / CSS

1.  Proper Formatting
2.  Meaning / Purposeful Markup
3.  Meaning / Purposeful Comments
4.  Consistent Naming Convention
    1.  BEM Modified
5.  Reduce Specificity
6.  Avoid Inline Styles
7.  External Style Sheets
8.  External JavaScript

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

There is a trend to nest extra div's for various reasons. This is especially noticeable with front end frame works. While I understand why libraries like Bootstrap need those div's, my concern is with their necessity overall. We should not be afraid of an extra div or span tag, but make it have meaning.

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

### Avoid Inline Styles

Inline styles should only apply to JavaScript manipulation.

## JavaScript

1.  Proper Formatting
2.  Meaningful Variables
3.  Meaningful Function Names
4.  Minimize Global Scope
5.  a

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

### Meaningful Varibles
