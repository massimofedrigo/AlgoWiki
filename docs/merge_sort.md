# Merge Sort <small style="color:gray; font-weight:normal;">(by John von Neumann, 1945)</small>

###### An efficient and stable algorithm, based on *divide and conquer* paradigm.

---

## 🧱 Properties

| Property               | Value                        |
|------------------------|------------------------------|
| **Worst-case time**    | $\mathcal{O}(n \log n)$       |
| **Average-case time**  | $\mathcal{O}(n \log n)$       |
| **Best-case time**     | $\mathcal{O}(n \log n)$       |
| **Space complexity**   | $\mathcal{O}(n)$ (auxiliary)  |
| **Stable**             | ✅ Yes                        |
| **In-place**           | ❌ No (requires extra memory) |

---

## 💡 Idea

Merge Sort is a sorting algorithm based on the *divide and conquer* paradigm. The core idea is to

- recursively divide the array into two halves
- sort each half
- merge the two sorted halves.

This approach guarantees a time complexity of $\mathcal{O}(n \log n)$ in all cases (best, average, and worst), making it highly efficient for large datasets.
Merge Sort is particularly useful when the data to be sorted does not fit entirely in main memory and must be handled using external memory (external sorting).

---

## ⚙️ Implementation

```cpp
template <typename T, std::size_t N, typename Compare = std::less<T>>
void merge(std::array<T, N>& array, std::size_t begin, std::size_t middle, std::size_t end,
           std::array<T, N>& aux, Compare comp = Compare{}) {
    std::size_t i = begin;
    std::size_t j = middle + 1;
    std::size_t k = 0;

    while (i <= middle && j <= end) {
        if (comp(array[i], array[j])) {
            aux[k++] = array[i++];
        } else {
            aux[k++] = array[j++];
        }
    }

    while (i <= middle) aux[k++] = array[i++];
    while (j <= end)    aux[k++] = array[j++];

    for (std::size_t m = 0; m < k; ++m) {
        array[begin + m] = aux[m];
    }
}

template <typename T, std::size_t N, typename Compare = std::less<T>>
void merge_sort(std::array<T, N>& array, std::size_t begin, std::size_t end,
                std::array<T, N>& aux, Compare comp = Compare{}) {
    if constexpr (N < 2) return;
    if (begin < end) {
        const std::size_t middle = (begin + end) / 2;
        merge_sort(array, begin, middle, aux, comp);
        merge_sort(array, middle + 1, end, aux, comp);
        merge(array, begin, middle, end, aux, comp);
    }
}

template <typename T, std::size_t N, typename Compare = std::less<T>>
void merge_sort(std::array<T, N>& array, Compare comp = Compare{}) {
    if constexpr (N < 2) return;
    std::array<T, N> aux = {};
    merge_sort(array, 0, N - 1, aux, comp);
}
```

---

## 📚 References

---

## 🔍 Curiosities

The merge sort algorithm was one of the first sorting algorithms invented that uses the *divide and conquer* strategy.
