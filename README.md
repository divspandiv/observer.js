# observer.js

```
function hasOwnProperty(obj, prop) {
  return Object.prototype.hasOwnProperty.call(obj, prop);
}

export default {
  _event: {},
  getEvent() {
    const pages = getCurrentPages();
    const currentPage = pages.pop();
    let events = this._event;
    if (currentPage) {
      currentPage._event = currentPage._event || {};
      events = currentPage._event;
    }
    return events;
  },
  emit(eventName, data) {
    const events = this.getEvent();
    if (!hasOwnProperty(events, eventName)) {
      return;
    }
    const fns = events[eventName];
    fns.forEach(fn => {
      fn.call(this, data)
    });
  },
  on(eventName, fn) {
    const events = this.getEvent();
    if (!hasOwnProperty(events, eventName)) {
      events[eventName] = [];
    }
    events[eventName].push(fn);
  },
  remove(eventName, fn) {
    const events = this.getEvent();
    if (!hasOwnProperty(events, eventName)) {
      return true;
    }
    const fns = events[eventName];
    console.log(fns);
    if (fn === undefined) {
      delete events[eventName];
    }
    const index = fns.indexOf(fns);
    if (index === -1) {
      return true;
    }
    fns.splice(index, 1);
  },
}
```
