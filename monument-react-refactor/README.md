# <img src="https://cloud.githubusercontent.com/assets/7833470/10899314/63829980-8188-11e5-8cdd-4ded5bcb6e36.png" height="60"> Monument Refactor (React)


## Overview

#### What is this lab?

Remember our Monument magazine website from the first week? Today we're going to modernize that project. It is now time to refactor our code for use with a modern front-end framework: React!

**The objective of this lab is to:**

* Refactor a static html site to use a component-based approach
* Familiarize yourself with React's filesystem and architecture on your terms
* Create reusable, robust codebase that will serve as a boilerplate for other work
* Continually grow the *Monument* brand until you are sick of light-blue branding styles

To refactor your Monument project, first **ensure you have the static version of Monument provided in this github repo** labeled `starter-static-site`.

**Suggested components for `index.html`:**
   
    - NavBar
    - Index
      - Hero/Header
      - Archive
        - Article
        - Article
        - Article
      - About
      - VisualGuide/Gallery
      - Contact
    - Footer

**Suggested components for `blog.html`:**
   
    - NavBar
    - Blog
      - PostList
        - Post
        - Post
        - Post
      - About
      - Issues
      - Comment
    - Footer


Keep components as large as possible until you begin to see opportunities to capitalize on repetition or obvious semantic separations, such as articles, sections, header/main/footer, etc. This will keep your workflow comprehensive and straightforward.  One early but major pitfall of React development is the tendency to prematurely optimize components to their smallest kernels. Taking the time to work incrementally ensures consistent code.

## Monument Refactor Guide
We'll refactor most of `index.html` as a group but it will be up to you to continue the refactoring work for the rest of this page as well as `blog.html` as your homework.

## We Do: Getting Started
1. Clone down [this repo](https://git.generalassemb.ly/sf-wdi-48/monument-react-refactor)

2. Run:
```
$ create-react-app statue-magazine
$ cd statue-magazine/
$ npm start
```

3. Confirm working application at localhost:3000 (you should see a spinning React logo)

4. Stop and break down the problem.
	 - Beginning with the largest pieces, what are some areas of `index` that stick out as potential Components?
	 - Look for hints in the lesson notes and match them to Monument

5. Remove leftovers from `create-react-app` boilerplate
	- change `<title></title>`
	- remove code from `src/App.css`; replace with Monument’s `style.css`
	- Make `src/index.css` look like:
```css
/* Base Styles */
/* =========== */
* {
    box-sizing: border-box;
}

html {
    font-size: 15px;
}

body {
    font-family: 'Raleway', sans-serif;
    -webkit-font-smoothing: antialiased;
    margin: 0;
    text-transform: uppercase;
    letter-spacing: .02em;
    text-align: center;
    color: #44545E;
}
```
> make sure to remove these lines in `App.css` (no need for duplication)

- Make `App.js` look like:
```jsx
import React, { Component } from 'react';
import './App.css';

class App extends Component {
    render() {
        return (
            <div className="App">

            </div>
        );
    }
}

export default App;
```

6. Confirm no errors on localhost and commit our changes so far. We’re about to build our first component, NavBar.


## Getting To Work: The NavBar Component
1. In `App.js`, add our first component: `<NavBar />`
```jsx
…
<div className="App">
    <NavBar />
</div>
…
```
- notice the error on localhost once we add this <NavBar /> component
- let’s fix it by building out the NavBar component and we’ll start by importing the component at the top of this file

2. Import NavBar (even though it doesn’t technically exist yet)
```jsx
import React, { Component } from 'react';
import './App.css';
import NavBar from './NavBar/NavBar'
```
- notice the new error on localhost
- let’s fix it by adding component code for a NavBar at `/src/NavBar/NavBar.js`

3. In `NavBar.js`:
```jsx
import React, { Component } from 'react';
import './NavBar.css';

class NavBar extends Component {
    render() {
        return (

        )
    }
}

export default NavBar;
```
- what are the similarities in this file compared to `App.js`
- given that we saw `App.js`’s return statement handle JSX (which looks a lot like regular HTML), what should we expect to put in the return statement of `NavBar.js`

4. Add the appropriate JSX to NavBar’s return statement
```jsx
…
class NavBar extends Component {
    render() {
        return (
            <nav>
                <a className="hamburger" href="/">
                    <i className="fa fa-bars"></i>
                </a>
                <ul>
                    <li><a href="index.html#about">About</a></li>
                    <li><a href="index.html#gallery">Gallery</a></li>
                    <li><a href="blog.html">Blog</a></li>
                    <li><a href="index.html#contact">Contact</a></li>
                </ul>
            </nav>
        );
    }
}
…
```
- no more errors on but not a great looking start to this either
- let’s add some css at `NavBar.css`
```css
nav {
	position: fixed;
	top: 0;
	left: 0;
	right: 0;
	background-color: white;
	z-index: 100;
}

nav li {
	display: inline-block;
}

nav a {
	font-weight: 600;
	letter-spacing: 0.75px;
	letter-spacing: .05rem;
	padding: 3px 60px;
	padding: .2rem 4rem;
	display: inline-block;
	border-bottom: none;
	text-transform: uppercase;
}

.hamburger {
	display: none;
}
```

6. Confirm the style is fixed and now would be a great time to commit our changes.

  
#### You Do: The Footer Component
In the last section we built the NavBar component and, as the only other shared component on the Monument page, the Footer is the next logical step. Thinking about what makes a component shouldn’t stop at the level of an individual page, we also need to consider shared components among multiple pages.

Following the same pattern as `<NavBar />`, but using code specific to the footer, build out a new `<Footer />` component.

Don’t be afraid to build this out on your own and make mistakes. In a few minutes we’ll go through it together as a group and make sure we’re all on the same page.

#### We Do: The Index Component and Beyond
1. As we’ve done twice already, invoke an `<Index />` component in `App.js`, import a corresponding module and file, create that file and a sibling stylesheet of the same name

2. In our `<Index />` component, copy and paste the remaining html code from `landing.html` in our starter app.

Stop.
- Does anything feel weird about this? Compare this new Index component to our previous NavBar and Footer components? Does this component follow the rules of FIRST?
- Can we make it better? Of course we can, with even more components.

3. Remove all JSX in the `return` statement of our Index component and replace with the following:
```jsx
import React, { Component } from 'react';
import Header from './Header/Header';

class Index extends Component {
    render() {
        return (
            <div>
                <Header />
            </div>
        )
    }
}
…
```
- This workflow should feel familiar. What are the next steps for this Header component and for the rest of the components on the page?

4. Continue the refactor project using the workflow demonstrated over the last few components.


**Note:** When you move on to the Blog page you may be wondering how to display it. You’ll notice the links to blog don’t actually take us to that page. We’ll be covering this more when we talk about React Router but for now you can comment out the `<Index />` component to hide it while working on the `<Blog />` component and vice versa.


**Stretch**
1. Design and build a Team page for Statue Magazine’s staff, keeping with the theme of the site and reusing already existing components where applicable.
