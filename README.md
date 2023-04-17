# twitter-unlike-ulikes


```Javascript
var wrapperSelector  = ".css-1dbjc4n"
var elementsSelector =     ".css-901oao.r-1awozwy.r-6koalj.r-37j5jr.r-a023e6.r-16dba41.r-1h0z5md.r-rjixqe.r-bcqeeo.r-o7ynqc.r-clp7b1.r-3s2u2q.r-qvutc0[style='color: rgb(249, 24, 128);']"


class Queue {
  constructor() {
    this.items = [];
  }

  enqueue(item) {
    this.items.push(item);
  }

  dequeue() {
    if (this.isEmpty()) {
      return null;
    }
    return this.items.shift();
  }

  isEmpty() {
    return this.items.length === 0;
  }
}

async function runProcess() {
  let queue = new Queue();

  const getUniqueElements = (elements, seen) => {
    const uniqueElements = [];
    elements.forEach((element) => {
      if (!seen.has(element)) {
        uniqueElements.push(element);
        seen.add(element);
      }
    });
    return uniqueElements;
  };

  const initialElements = document.querySelectorAll(wrapperSelector)[0].querySelectorAll(elementsSelector);

  const seenElements = new Set();
  const uniqueInitialElements = getUniqueElements(initialElements, seenElements);
  uniqueInitialElements.forEach((element) => queue.enqueue(element));

  while (!queue.isEmpty()) {
    const element = queue.dequeue();
    element.click();
    element.scrollIntoView({ behavior: "smooth" });

    await new Promise((resolve) => setTimeout(resolve, 1000));

    const newElements = document.querySelectorAll(wrapperSelector)[0].querySelectorAll(elementsSelector);

    const uniqueNewElements = getUniqueElements(newElements, seenElements);
    uniqueNewElements.forEach((newElement) => queue.enqueue(newElement));
  }
}

runProcess();

```
