## Install

```
npm install @banno/web-component-router
```

## Defining Routes

- Set up in page.js

```
/**
 * @fileoverview
 *
 * Route tree definition
 *
 *           ___APP-ELEMENT___
 *          /                 \
 *     LOGIN-PAGE     ___MAIN-LAYOUT_____
 *                   /                   \
 *           MAIN-DASHBOARD         DETAIL-VIEW
 */

const RouteData = require('@banno/web-component-router/lib/route-data');
const RouteTreeNode = require('@banno/web-component-router/lib/route-tree-node');

const dashboard = new RouteTreeNode(
    new RouteData('MainDashboard', 'MAIN-DASHBOARD', '/'));

const detailView = new RouteTreeNode(
    new RouteData('DetailView', 'DETAIL-VIEW', '/detail/:viewId', ['viewId']));

// This is an abstract route - you can't visit it directly.
// However it is part of the dom tree
const mainLayout = new RouteTreeNode(
    new RouteData('MainLayout', 'MAIN-LAYOUT', ''));

mainLayout.addChild(dashboard);
mainLayout.addChild(detailView);

// This is an abstract route - you can't visit it directly.
// However it is part of the dom tree
// It also does not require authentication to view
const app = new RouteTreeNode(
    new RouteData('App', 'APP-ELEMENT', '', [], false));

app.addChild(mainLayout);

const loginPage = new RouteTreeNode(
    new RouteData('Login', 'LOGIN-PAGE', '/login', [], false));

app.addChild(loginPage);

module.exports = app;
```

### Dealing with the above code

```
// This is an abstract route - you can't visit it directly.
// However it is part of the dom tree
const mainLayout = new RouteTreeNode(
    new RouteData('MainLayout', 'MAIN-LAYOUT', ''));
```
So basically this serves as part of the path but going directly to it doesn't actually have a view. So the first two parts are parts of the tree, but they don't contain anything.
