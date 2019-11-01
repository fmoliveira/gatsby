---
title: Understanding React Rehydration
---

One of the central ideas of Gatsby is that HTML content is statically generated--using React DOM server-side APIs. A follow up key feature is that this static HTML content can then be _enhanced_ with client-side JavaScript via React hydration which allows for [app-like features](/docs/adding-app-and-website-functionality/) in Gatsby sites.

The steps taken to deliver a built site to the browser are discussed below:

## Build and render static assets

Running `gatsby build` starts up a Node.js server that processes your site: creating a GraphQL schema for your site, fetching data that your pages will pull in by [extracting queries](/docs/query-extraction/) from your code and [executing them](/docs/query-execution/), and [rendering each page's HTML](/docs/html-generation/).

_The ["Overview of the Gatsby Build Process" conceptual guide](/docs/overview-of-the-gatsby-build-process/) helps explain what's happening at each step in the build process_

All of this data is gathered during the build and written into the `/public` folder. You can [customize Gatsby's configurations](/docs/customization/) for `babel`, `webpack`, as well as the HTML generated by your build in order for finer grained tweaks in regards to how your site gets built.

## Invoke the `ReactDOM.hydrate` method

The `hydrate()` method is called from `ReactDOM`, which according to the [React docs](https://reactjs.org/docs/react-dom.html#hydrate) is:

> Same as [render()](https://reactjs.org/docs/react-dom.html#render), but is used to hydrate a container whose HTML contents were rendered by [ReactDOMServer](https://reactjs.org/docs/react-dom-server.html).

This means that the browser can "pick up" where the server left off with the contents created by Gatsby in the `/public` folder and mount the site in the browser just like any other React app would be. Since the data and structure of the pages is already written out, it's not necessary for Gatsby to go to another asking for HTML or other data.

## Transfer rendering to the React reconciler

After ReactDOM hydrates the content, the React reconciler can take over and diff the tree of elements. It then becomes responsible for making updates in the UI based on changing state or props.

## Additional resources

- [Rendering on the Web](https://developers.google.com/web/updates/2019/02/rendering-on-the-web) from Google