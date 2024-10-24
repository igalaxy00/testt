Вопрос №1
 def isEven(value):return value&1==0
Объяснение
Плюсы:
Использование оператора & определяет четность числа без деления, что может быть быстрее для некоторых систем на низком уровне.
Этот метод может быть более понятным для тех, кто знаком с побитовой арифметикой.
Минусы:

Для большинства случаев, использование оператора % более интуитивно понятно.
В современных интерпретаторах Python разница в производительности может быть незначительной, и использование % может быть более предпочтительным из-за его ясности.

Вопрос №2
Реализация 1: С использованием списка
class CircularBufferList:
    def __init__(self, size):
        self.size = size
        self.buffer = []
 def add(self, item):
        if len(self.buffer) < self.size:
            self.buffer.append(item)
        else:
            self.buffer.pop(0)  # Удаляем первый элемент
            self.buffer.append(item)

    def get(self):
        return self.buffer

buffer = CircularBufferList(3)
buffer.add(1)
buffer.add(2)
buffer.add(3)
buffer.add(4)  # 1 будет удален
print(buffer.get())  # [2, 3, 4]

Реализация 2: С использованием collections.deque

from collections import deque
class CircularBufferDeque:
    def __init__(self, size):
        self.buffer = deque(maxlen=size)

    def add(self, item):
        self.buffer.append(item)

    def get(self):
        return list(self.buffer)

buffer = CircularBufferDeque(3)
buffer.add(1)
buffer.add(2)
buffer.add(3)
buffer.add(4)  # 1 будет удален
print(buffer.get())  # [2, 3, 4]
Объяснение
Плюсы реализации списка(1 реализации):

Простота и понятность кода.
Легко реализовать, если не нужна высокая производительность.
Минусы реализации с использованием списка:
Удаление первого элемента требует сдвига всех оставшихся элементов, что приводит к сложности O(n).
Плюсы реализации с использованием deque:
collections.deque оптимизирован для операций добавления и удаления с обеих сторон, что делает его более эффективным (O(1) для добавления и удаления).
Минусы реализации с использованием deque:
Немного больше кода для импорта и использования, но не думаю что это значительно
по сравнению с преимуществами.
Вопрос №3
Алгоритм сортировки
 Используем встроенную функцию sorted(), которая использует Timsort

array = [3, 6, 8, 10, 1, 2, 1]
sorted_array = sorted(array)
print(sorted_array)

 Или можно использовать метод .sort() для списков
array.sort()
print(array)
def merge_sort(arr):
    if len(arr) <= 1:
        return arr mid = len(arr) // 2
    left_half = merge_sort(arr[:mid])
    right_half = merge_sort(arr[mid:])

    return merge(left_half, right_half)

def merge(left, right):
    sorted_array = []
    i = j = 0

    while i < len(left) and j < len(right):
        if left[i] < right[j]:
            sorted_array.append(left[i])
            i += 1 else:
            sorted_array.append(right[j])
            j += 1 sorted_array.extend(left[i:])
    sorted_array.extend(right[j:])
    
    return sorted_array

array = [3, 6, 8, 10, 1, 2, 1]
sorted_array = merge_sort(array)
print(sorted_array)


Преимущества Merge Sort:
Стабильность: Merge Sort является стабильным алгоритмом сортировки

Предсказуемая производительность: В отличие от Quick Sort, который может иметь худший случай O(n^2), Merge Sort всегда работает за O(n log n), что делает его более предсказуемым в производительности.

Работа с большими объемами данных: Merge Sort хорошо работает с большими объемами данных

Недостатки Merge Sort:
Дополнительная память: Merge Sort требует O(n) дополнительной памяти для хранения временных массивов при слиянии, что может быть проблемой для больших массивов.

Скорость на небольших массивах: На небольших массивах Merge Sort может быть медленнее, чем такие алгоритмы, как Insertion Sort Timsort, из-за дополнительных расходов на рекурсию и слияние.
