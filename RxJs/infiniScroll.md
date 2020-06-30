# infinit scroll exemple

```javascript
import { debounceTime, filter, map, pairwise, startWith } from "rxjs/operators";
import { THeightElem } from "../types";

const onScrollObs$ = fromEvent(window, "scroll");
const onScrollDashbord$ = onScrollObs$.pipe(
  debounceTime(100),
  map(() => {
    //scrollHeight => hauteur du contenu de l'élément racine du document
    const scrollHeight: number = document.documentElement.scrollHeight;
    //pageYOffset => the number of pixels the document is currently scrolled
    const pageYOffset: number = window.pageYOffset;
    //clientHeight => hauteur du client
    const clientHeight: number = document.documentElement.clientHeight;
    return { scrollHeight, pageYOffset, clientHeight };
  }),
  filter((obj: THeightElem): boolean => {
    const val: number = obj.scrollHeight - obj.pageYOffset - obj.clientHeight;
    return val < 200;
  }),
  startWith({
    scrollHeight: 0,
    pageYOffset: 0,
    clientHeight: 0,
  }),
  pairwise(),
  filter(([prev, cur]: THeightElem[]): boolean => {
    const val: number = cur.scrollHeight - cur.pageYOffset - cur.clientHeight;
    return prev.scrollHeight !== cur.scrollHeight && val < 200;
  })
);
export default onScrollDashbord$;
```

ou

````javascript
this.scroll$ = fromEvent(window, 'scroll').pipe(
      debounceTime(20),
      map(
        () =>
          document.documentElement.scrollHeight -
          window.pageYOffset -
          document.documentElement.clientHeight,
      ),
      distinctUntilChanged(),
      filter(remaining => remaining < 500),
      exhaustMap(() => API CALLS)
      takeWhile(res => res.length > 0),
    )
    ```
````
