# Bubble Sort <small style="color:gray; font-weight:normal;">(by Unknown, 1956)</small>

###### A simple sorting algorithm that repeatedly swaps adjacent elements.

---

## 🧱 Properties

| Property               | Value                        |
|------------------------|------------------------------|
| **Worst-case time**    | $\mathcal{O}(n^2)$           |
| **Average-case time**  | $\mathcal{O}(n^2)$           |
| **Best-case time**     | $\mathcal{O}(n)$             |
| **Space complexity**   | $\mathcal{O}(1)$ (auxiliary) |
| **Stable**             | ✅ Yes                        |
| **In-place**           | ✅ Yes                        |

---

## 💡 Idea

Bubble Sort is a straightforward sorting algorithm that repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order.
The algorithm gets its name because smaller elements bubble to the top of the list with each pass.

- Compare adjacent elements
- Swap if needed
- Repeat until the list is sorted

While it is easy to understand and implement, Bubble Sort is inefficient on large datasets. However, it can be optimized to detect if the array is already sorted.

---

## ⚙️ Implementation

```cpp
template<typename T, std::size_t N, typename Compare = std::less<T>>
void bubble_sort(std::array<T, N>& array, Compare comp = Compare{}) {
   if constexpr (N < 2) return;
   for (std::size_t i=0; i<N-1; i++) {
      for (std::size_t j=0; j<N-i-1; j++) {
         if (comp(array[j+1], array[j])) {
            std::swap(array[j], array[j+1]);
         }
      }
   }
}
```

---

## 📚 References

---

## 🔍 Curiosities

Despite being one of the least efficient sorting algorithms, Bubble Sort is often taught for its educational value and simplicity.
