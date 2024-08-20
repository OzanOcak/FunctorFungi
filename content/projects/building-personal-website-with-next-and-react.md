---
title : 'Building Personal Website With Next and React'
date : 2024-08-19T22:53:13-04:00
draft : false
author: ["Ozan"]
categories: ["programming"]
tags: ["Next","React"]
description: "Building Personal Website With Next and React"
weight: 1
slug: ""
draft: false # draft or not
cover:
    image: "/img/projects/01/personalwebsite.png"
    caption: "screenshot of my website"
    alt: "screenshot of my website"
    relative: false
showToc: false

---

I have built my personal website with Next framwork and React library, you can visit my website at **[oocak.com](https://www.oocak.com)**

React and Next.js are a great combination for building modern web applications. Here's why they make a perfect couple and a tutorial on how to set up a Next.js app with a simple React user interface.

### React and Next.js

**1. Server-side Rendering (SSR):** Next.js provides server-side rendering out of the box, which can improve the initial load time and search engine optimization (SEO) of your application, as opposed to a purely client-side React application.

**2. Static Site Generation (SSG):** Next.js allows you to pre-render pages at build-time, creating highly performant "static" pages that can be served directly from a CDN.

**3. Routing and File-based Routing:** Next.js has a file-based routing system, which makes it easy to set up and maintain the navigation structure of your application.

**4. Automatic Code Splitting:** Next.js automatically splits your application's code, reducing the amount of JavaScript that needs to be downloaded on each page load.

**5. Image Optimization:** Next.js provides built-in image optimization, which can significantly improve the performance of your application.

**6. Seamless Integration with React:** Next.js is built on top of React, so you can leverage all the power and flexibility of the React ecosystem.
Tutorial: Setting up a Next.js App with a Simple React User Interface

```console
brew install node
npx create-next-app my-app
```
This will create a new directory called my-app with the necessary files and folders for a Next.js application.

**Develop the React User Interface:** Next.js uses the pages directory to define your application's routes. Open the pages directory and create a new file called index.js. In this file, you can build your React user interface:

```jsx
import React from 'react';

const HomePage = () => {
  return (
    <div>
      <h1>Welcome to my Next.js App</h1>
      <p>This is a simple React user interface built with Next.js.</p>
    </div>
  );
};

export default HomePage;
```

**Run the Development Server:** In your terminal, navigate to the my-app directory and run the following command to start the development server:

```console
npm run dev
```
This will start the Next.js development server and open your application in your default web browser.

**Static Site Generation:** Create pre-rendered pages at build-time using the getStaticProps or getStaticPaths functions.

**Server-side Rendering:** Render pages on the server using the getServerSideProps function.

**API Routes:** Create serverless API routes using the pages/api directory.

**Styling:** Integrate CSS, Sass, or other styling solutions into your Next.js application.

**Deployment:** Deploy your Next.js app to popular hosting platforms like Vercel, Netlify, or AWS.
By combining the power of React and the features of Next.js, you can create high-performance, scalable web applications with a seamless user experience.
