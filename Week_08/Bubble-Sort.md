Bubble-Sort

```javascript
    /**
    * @param {array} arr
    * @return {array}
    */
    function bubbleSort(arr) {
      if (arr.length <= 1) {
        return arr;
      }
      const len = arr.length;
      let change;
      for (let i = 0; i < len - 1; i++) {
        change = true;
        for (let j = 0; j < len - 1 - i; j++) {
          if (arr[j] > arr[j + 1]) {
            [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]];
            change = false;
          }
        }
        if (change) {
          break;
        }
      }
      return arr;
    }
```

