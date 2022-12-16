# **Односвязный список**
*Учебный проект Яндекс.Практикума*

Односвязный список ещё называют линейным однонаправленным списком. Эта структура данных состоит из элементов одного типа. Их логически связывают между собой указатели. Каждый элемент списка указывает на следующий, а последний — на nullptr. Хранятся элементы списка, как правило, в динамической памяти.

Структура односвязного списка такова, что передвигаться по его элементам можно только в прямом направлении. Узнать адрес предыдущего элемента, опираясь лишь на содержимое текущего элемента, невозможно.

**Односвязный список допускает следующие операции:**
- вставка элемента в начало или конец списка,
- вставка элемента после некоторого элемента списка,
- удаление элемента, следующего за данным элементом списка,
- проверка списка на пустоту,
- определение количества элементов в списке.

**Достоинства односвязного списка:**

вставка и удаление элемента выполняются за константное время, то есть не зависят от количества элементов и позиции вставляемого или удаляемого элемента;
размер списка ограничен лишь объёмом доступной памяти.

**Недостатки односвязного списка следуют из особенностей его структуры:**

Узнать адрес элемента по его порядковому номеру — операция линейной сложности. Чтобы определить адрес N-го элемента списка, нужно последовательно перебрать все N-1 элементов, начиная с первого элемента.
Неэффективное расходование памяти: помимо данных, каждый элемент списка хранит указатель на следующий элемент. Кроме того, при каждом создании объекта в динамической памяти пара десятков байт расходуется на поддержание структуры кучи.
Не такая высокая эффективность вставки и удаления. Каждая вставка и каждое удаление обращаются к операциям работы с кучей: new или delete. Считается, что эти операции работают за константное время, однако константа может быть достаточно большой. При этом выполняется сложный код синхронизации между потоками, и могут быть задействованы низкоуровневые механизмы работы с памятью.
Соседние элементы списка могут располагаться в памяти непоследовательно, что снижает эффективность работы кэш-памяти.


В классе списка разработана поддержка перебора элементов контейнера SingleLinkedList посредством шаблонного класса BasicIterator, на основе которого объявлены константный и неконстантный итераторы списка.
В классе списка также реализованы константная и неконстантная версии методов begin и end, которые возвращают итераторы на первый элемент контейнера и позицию, следующую за последним элементом. Чтобы получать константные итераторы было удобно, реализованы методы cbegin и cend.


**В классе односвязного списка реализован следующий функционал:**
- Операции сравнения ==, !=, <, >, <=, >=;
- Обмен содержимого двух списков с использованием метода swap и шаблонной функции swap;
- Конструирование односвязного списка на основе initializer_list. Последовательность элементов созданного списка и initializer_list одинакова;
- Надёжные конструктор копирования и операция присваивания. Операция присваивания обеспечивает строгую гарантию безопасности исключений. Если в процессе присваивания будет выброшено исключение, содержимое левого аргумента операции присваивания остаётся без изменений.
- Метод PushFront предоставляет строгую гарантию безопасности исключений: если в процессе работы метода будет выброшено исключение, состояние списка останется таким же, как до вызова метода.
- Метод Clear очищает список и не выбрасывает исключений.
- Метод PopFront. Удаляет первый элемента непустого списка за время O(1). Не выбрасывает исключений.
- Метод InsertAfter. За время O(1) вставляет в список новое значение следом за элементом, на который ссылается переданный в InsertAfter итератор. Метод обеспечивает строгую гарантию безопасности исключений.
- Метод EraseAfter. За время O(1) удаляет из списка элемент, следующий за элементом, на который ссылается переданный в InsertAfter итератор. Не выбрасывает исключений.
- Методы before_begin и cbefore_begin. Возвращают итераторы, ссылающиеся на фиктивную позицию перед первым элементом списка. Такой итератор используется как параметр для методов InsertAfter и EraseAfter, когда нужно вставить или удалить элемент в начале списка.
