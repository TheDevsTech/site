---
title: "What is React and How Does It Work"
date: 2020-01-06T08:26:52+06:00
draft: true
authors:
- Md. Rubayet Hossain
categories:
- JavaScript
- React
- Frontend Development
description: A short introduction on React
tags:
- javascript
- react
- frontend
---

So if you are into the web development world or you just started learning web designing, you may hear about React. On this post you will know what is React and how does it **react**. I am considering the audience of this post at least know HTML, CSS and JavaScript! 

# What is React?

React is a JavaScript library to build interactive User Interfaces. It is maintained by Facebook and a community of individual developers and companies! There has another framework called React Native which is used for building mobile apps. The interesting thing here is if you learn React, you can write React Native too. So you can develop website as well as mobile applications! Let's know about the two core characteristics of React.

### React is Declarative
What is Declarative? Declarative code represents what a line of code does in an app. Lets consider the following code snippets.

```html
<App>
    <Header />
    <Wrapper>
        <Sidebar />
        <Content />
    </Wrapper>
    <Footer />
</App>
```
From the above it is clear that what a line of code represents. The `App` tag tells it's the starting of an app, `Header` and `Footer` declares header and footer respectively and so on. 

### React is Component Based
Everything in React is Component. But what is a component? On the above code the `App`, `Header`, `Content`, `Wrapper` etc are Component. Let's see a simple Component definition,

```jsx
class Header extends React.Component{
    render(){
        return(
            <header>
                This is a Component
            </header>
        )
    }
}
```
If you check the `return` statement if might looks familiar to you. Yes! It's a simple `html` statement. React renders the `html` statement you return from a component. But there has more to know about Component. We will know about it shortly. 

