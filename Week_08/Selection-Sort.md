选择排序

```javascript
    /**
    * @param {array} arr
    * @return {array}
    */
    function selectionSort(arr) {
      if (arr.length <= 1) {
        return arr;
      }
      const len = arr.length;
      let minIndex;
      for (let i = 0; i < len - 1; i++) {
        minIndex = i;
        for (let j = i + 1; j < len; j++) {
          if (arr[minIndex] > arr[j]) {
            minIndex = j;
          }
        }
        [arr[i], arr[minIndex]] = [arr[minIndex], arr[i]];
      }
      return arr;
    }
```

