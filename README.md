# Redone Observable

### Reading values from an observable
```js
import { Autorun } from 'redone';
import { Sink } from 'redone-observable';
import Rx from 'rxjs/Rx';

const subject = new Rx.BehaviorSubject('test');
const sink = new Sink(subject);
Autorun.start(() => {
  console.log(sink.value);
});
// 'test'

subject.next('foo');
// 'foo'

sink.dispose();
subject.next('bar');
// (nothing printed)
```

### Pushing values through an observable
```js
import { Datum } from 'redone';
import { observe } from 'redone-observable';

const datum = new Datum('test');
const observable = observe(() => datum.get());
observable.subscribe(value => {
  console.log(value);
});
// 'test'

datum.set('foo');
// 'foo'
```
