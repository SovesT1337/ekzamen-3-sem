# ekzamen-3-sem
## 1) Двусвязный список: поиск элемента по значению, вставка элемента, удаление элемента. Реализация функции удаления элемента из двусвязного списка. Основные методы std::list. Пример работы с std::list
## 2) Класс std::map. Внутренняя реализация map, его основные методы. Сложность поиска, сортировки, удаления элемента, добавления элемента. Пример работы с std::map
## 3) Класс std::set. Внутренняя реализация set, его основные методы. Сложность поиска, сортировки, удаления элемента, добавления элемента. Пример работы с std::set
## 4) Класс std::unordered_map. Внутренняя реализация unordered_map, его основные методы. Сложность поиска, сортировки, удаления элемента, добавления элемента. Пример работы с std:: unordered_map
## 5) Класс std::vector. Внутренняя реализация vector, его основные методы. Сложность поиска, сортировки, удаления элемента, добавления элемента. Пример работы с std::vector. Особенность std::vector<bool>.
## 6) Парадигмы ООП. Полиморфизм (статический, динамический). Инкапсуляция. Наследование. Примеры.
## 7) Разработка обобщенных типов: шаблоны С++. Инстанцирование. Спецификация шаблонов. Примеры.
## 8) Итераторы: определение, назначение, преимущества. Итераторы прямого доступа, итераторы ввода, итераторы вывода, двунаправленные итераторы, прямой итератор. Примеры.
## 9) Современный С++: auto, decltype, range base loop, nullptr, constexpr, enum class, if constexpr.
## 10) Современный С++: static_assert, initializer_list, default, final, override, using
## 11) Современный С++: std::optional, std::variant, std::any, std::string_view. Примеры использования
## 12) Лямбда-функции, функторы, указатели на функции, std::functional. Примеры использования std::functional. Примеры использования лямбда-функций.
## 13) R-value ссылки. Семантика перемещения. std::move, std::forward. Пример.
  
  Rvalue ссылки - техническое расширение языка C++. Они позволяют компилятору определить, когда необходимо использовать перемещение, вместо копирования. 
  
  Семантика перемещения позволяет компиляторам заменять дорогостоящие операции копирования "дешевыми" операциями перемещения. Семантика также позволяет создавать типы, которые концептуальлно поддерживают только опферации перемещения. 
  
  std::move безусловно приводит аргумент фк ravalue ссылке.
  
  ```cpp
    std::string str = "Salut";
    std::vector<std::string> v;
 
    v.push_back(str);
    std::cout << "After copy, str is " << str << '\n';
 
    v.push_back(std::move(str));
    std::cout << "After move, str is " << str << '\n';
 
    std::cout << "The contents of the vector are { " << std::quoted(v[0])
                                             << ", " << std::quoted(v[1]) << " }\n";
  ```
  
  Функция std::forward применяется при идеальной передаче (perfect forwarding). Идеальная передача позволяет создавать функции-обертки, передающие параметры без каких-либо изменений (lvalue передаются как lvalue, а rvalue – как rvalue).
  
  ```cpp
  void push(T&& value) {
    T* data = new T[length];
    if (length) {
      for (unsigned int i = 0; i < length; ++i) data[i] = forward<T>(ptr[i]);
    }
    delete[] ptr;
    ++length;
    ptr = new T[length];
    for (unsigned int i = 0; i < length - 1; ++i) ptr[i] = forward<T>(data[i]);
    delete[] data;
    ptr[length - 1] = forward<T>(value);
  }
  ```
  
## 14) Обработка ошибок с использованием механизма обработки исключений. RAII. Примеры классов, использующих RAII. Ключевое слово noexcept.
  
  Пример обработки ошибок с использованием механизма обработки исключений:
  ```cpp
  try
{
    // Здесь мы пишем стейтменты, которые будут генерировать следующее исключение
    throw -1; // типичный стейтмент throw
}
 
  catch (int a)
{
    // Обрабатываем исключение типа int
    std::cerr << "We caught an int exception with value" << a << '\n';
}
  ```
  
  Идиома RAII
Resource Acquisition Is Initialization - идиома объектно-ориентированного программирования, смысл которой заключается в том, что получение некоторого ресурса неразрывно совмещается с инициализацией объекта, а освобождение — с уничтожением.
  
  RAII
Другими словами, выделяем память (или любой другой ресурс) в конструкторе некого объекта, а освобождаем - в деструкторе.
  
  Классы использующие RAII: boost::scooped_ptr, std::unique_ptr, std::shared_ptr, std::weak_ptr.

  Noexept - метод с помощью которого программист сообщает компилятору, должна ли функция создавать исключения. 
  
## 15) RAII. «Умные» указатели. std::shared_ptr. Примеры.
  
  RAII см. 14 вопрос

  Указатель std::shared_ptr используется для управления ресурсами путем совместного владения, т.е. объект, на который указывает shared_ptr, унитожится только после того, как не останется ни одного shared_ptr ссылающегося на него.
  
  std::shared_ptr является копируемым и перемещаемым.
  
  Подсчет ссылок в shared_ptr построен с помощью атомарного счетчика, Можно безопасно использовать указатели лна один и тот же объект из разных потоков. 
  
  ``` cpp
  std::shared_ptr ptr(new Image("~/Photo.png"));
  
  std::shared_ptr another_ptr = ptr;
  assert(ptr != nullptr);
  assert(another_ptr != nullptr);
  
  std::yet_another_ptr = std::move(ptr);
  assert(ptr == nullptr);
  assert(yet_another_ptr != nullptr);
  ```

## 16) RAII. «Умные» указатели. std::unique_ptr. Примеры.\
  
  RAII см. 14 вопрос
  
  std::unique_ptr - владеет объектом, на который указывает, т.е. отвечает за уничтожение объекта и освобождение памяти.
  
  std::unique_ptr - является некопируемый, но перемещаемым объектом. При попытке копировать std::unique_ptr получим ошибку компиляции.
  
  По умолчанию, std::unique_ptr имеет тот же размер, что и обычные указатели. Для большинства операций выполняются точно такие же команды. Следовательно std::unique_ptr можно использовать, когда важны расход памяти и времени.
  
  Совместим с stl-контейнером. Поддерживает custom deleater.
  
  ``` cpp
  std::unique_ptr ptr(new Image("~/photo.png"));
  std::unique_ptr amother_ptr = std::move(ptr);
  assert(ptr == nullptr);
  assert(another_ptr != nullptr);
  ```
  ## 17) RAII. «Умные» указатели. std::weak_ptr. Примеры.
  
  RAII см. 14 вопрос
  
  Умный указатель std::weak_ptr был разработан для решения проблемы «циклической зависимости». std::weak_ptr является наблюдателем — он может наблюдать и получать доступ к тому же объекту, на который указывает std::shared_ptr (или другой std::weak_ptr), но не считаться владельцем этого объекта.
  
  ```cpp
  weak_ptr<Parent> parentWeakPtr_ = parentSharedPtr;
  shared_ptr<Parent> tempParentSharedPtr = parentWeakPtr_.lock();
if( !tempParentSharedPtr ) {
  // yes, it may fail if the parent was freed since we stored weak_ptr
} else {
  // do stuff
}
```
  
## 18) Сетевое взаимодействие. Berkley sockets. Основные функции для работы с сокетами
## 19) Сетевое взаимодействие. Сокеты. Библиотека boost asio.
## 20) Управление потоками. Состояния гонок в интерфейсе структур данных. Класс std::future, функция std::async.
## 21) Переключение контекста потоков. Класс std::thread. Ключевое слово thread_local. Примеры использования thread_local.
## 22) Переключение контекста потоков. Класс std::thread. Ключевое слово thread_local. Примеры использования std::thread.
## 23) Синхронизация потоков. Состояние гонок. Классы std::mutex, std::lock_guard, std::unique_lock. Функция std::lock. Примеры использования мьютексов.
## 24) Синхронизация потоков. Состояние гонок. Классы std::recursive_mutex, boost::shared_mutex, std::unique_lock. Функция std::lock. Пример использования std::unique_lock
## 25) Класс std::condition_variable. Потокобезопасные структуры данных с блокировками.
## 26) Синхронизация потоков. Пул потоков. Класс std::condition_variable. Примеры работы с std::condition_variable
## 27) Управление потоками. Состояния гонок в интерфейсе структур данных. Класс std::future, функция std::async
## 28) Атомарные операции. Классы std::atomic, std::atomic_flag. Примеры работы с std::atomic
## 29) Шаблоны проектирования: фабричный метод. Пример реализации «простой фабрики» и «фабричного метода».
  
  Шаблон проектирования - повторяющаяся архитектурная конструкция, представляющая собой решение проблемы проектирования в рамках некоторого часто возникающего контекста.
  
  Паттерн "Простая фабрика" - это класс, в котором есть один метод с большим условным оператором, выбирающим создаваемый продукт.
  
  ```cpp
  struct Barrack {
  Unit* CreateUnit(UnitID unit_id) {
 
    switch (unit_id) {
      case UnitID::Knight:
        return new Knight();
      case UnitID::Archer:
        return new Archer();
      default:
        return nullptr;
    }
  }
};
  ```
  
  Паттерн "Фабричный метод" - это устройство классов, при котором подклассы могут переопределять тип создаваемого в суперклассе продукта.
  
  ```cpp
  struct Barrack {
  virtual Unit* CreateUnit() = 0;
 
  void Hire(Player& player) {
    auto* unit = CreateUnit();
    player.AddToArmy(unit);
  }
  
  struct KnightBarrack : public Barrack {
  Unit* CreateUnit() override {
    return new Knight();
  }
};
struct ArcherBarrack : public Barrack {
  Unit* CreateUnit() override {
    return new Archer();
  }
};
 
ArcherBarrack archer_barrack;
archer_barrack.Hire(player);
KnightBarrack knight_barrack;
knight_barrack.Hire(player);
};
  
  ```
  
## 30) Шаблоны проектирования: observer. Пример реализации «обозреватель».
## 31) Шаблоны проектирования: синглтон. Пример реализации Синглтона.
## 32) Асинхронное программирование. Плюсы и минусы. Сопрограммы. Функции обратного вызова.
## 33) Атомарные операции. Классы std::atomic. Структуры данных без блокировок. Реализация lock-free stack
  
  
