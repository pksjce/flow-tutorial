```javascript
/*
const routeMap = {
HOME: 'home',
}
*/
type RouteMap = {
  [string]: string
};

/*
const history ={
    length: globalHistory.length,
    action: "POP",
    location: initialLocation,
    createHref,
    push,
    replace,
    go,
    goBack,
    goForward,
    block,
    listen
  };
*/

type History = {
    length: number,
    action: "POP" | "PUSH" | "REPLACE",
    location: {
        pathname: string,
        search: string,
        hash: string,
        key:  string,
        state: string | void,
    },
    createHref: (href: string): string;
}

connectRoutes(history, routeMap);
```
