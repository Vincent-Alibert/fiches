# Mettre en pause un observable

```javascript
import { interval, Subject, merge, EMPTY } from "rxjs";
import {
  windowToggle,
  mergeAll,
  share,
  take,
  startWith,
  distinctUntilChanged,
  filter,
  flatMap,
  bufferToggle,
  map,
  pairwise,
} from "rxjs/operators";

export const pauseSubj$ = new Subject<boolean>();
const pause$ = pauseSubj$.pipe(distinctUntilChanged(), share());

export function startTest() {
  const time = interval(1000).pipe(
    take(20)
  );

  const pause = pause$.pipe(filter((v) => !v));
  const play = pause$.pipe(filter((v) => v));

  const result$ = merge(
    time.pipe(
      bufferToggle(play, () => pause),
      flatMap((x) => {
        console.log("bufferToggle x", x);
        return EMPTY;
      })
    ),
    time.pipe(
      windowToggle(pause, () => play),
      flatMap((x) => {
        return x;
      })
    )
  );
  // tricks pour déclencher le compte dès le départ
  setTimeout(() => {
    pauseSubj$.next(false);
  }, 0);

  // pour mettre simplement en pause (avec perte des valeurs) on remplace
  // const resulta$ par
  // const result$ = time.pipe(
  //   windowToggle(play, () => pause),
  //   mergeAll(1)
  // );

  return result$;
}
```
