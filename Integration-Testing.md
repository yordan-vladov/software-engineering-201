Интеграционното тестване е вид тестване, при което се проверява как различни части или модули на софтуерната система работят заедно. Целта е да се открият проблеми в взаимодействието между тези модули, като например грешки в комуникацията, неправилно предаване на данни или несъвместимост между компонентите. Това е важно, защото дори отделните модули да работят правилно поотделно, може да има проблеми, когато се комбинират.

## Проект за интеграционно тестване

Ще разработим прост проект - опростен уеб магазин. Проектът включва два модула: един за управление на продукти, един за управление на поръчки, един за потребители. След това ще тестваме как тези модули работят заедно.

### Създаване на модулите

####  Модул за управление на продуктите

Този модул съдържа функции за добавяне и търсене на продукти.

```python
# product_module.py

# База данни с продукти (речник)
products = {}

def add_product(product_id, name, price):
    """
    Добавя продукт в базата данни.
    """
    products[product_id] = {"name": name, "price": price}

def get_product(product_id):
    """
    Връща продукт по ID.
    """
    return products.get(product_id, None)
```

#### Модул за изчисляване на поръчки

Този модул изчислява общата цена на поръчка.

```python
# order_module.py

from product_module import get_product

def calculate_total_price(order_items):
    """
    Изчислява общата цена на поръчка.
    order_items е списък от tuples (product_id, quantity).
    """
    total = 0
    for product_id, quantity in order_items:
        product = get_product(product_id)
        if product:
            total += product["price"] * quantity
    return total
```

#### Модул за валидиране на потребители

Този модул валидира потребителски данни.

```python
# user_module.py

def validate_user(email, password):
    """
    Валидира потребителски данни.
    """
    if "@" not in email or len(password) < 6:
        return False
    return True
```

#### Основно приложение

Това е основното приложение, което интегрира всички модули.

```python
# main_app.py

from product_module import add_product
from order_module import calculate_total_price
from user_module import validate_user

def main():
    # Добавяне на продукти
    add_product(1, "Laptop", 1200)
    add_product(2, "Mouse", 20)

    # Валидиране на потребител
    if not validate_user("user@example.com", "password123"):
        print("Невалидни потребителски данни!")
        return

    # Създаване на поръчка
    order_items = [(1, 1), (2, 2)]  # 1x Laptop, 2x Mouse
    total_price = calculate_total_price(order_items)
    print(f"Обща цена на поръчката: ${total_price}")

if __name__ == "__main__":
    main()
```

### Интеграционно тестване

Сега ще напишем интеграционни тестове, за да проверим дали всички модули работят заедно правилно.

```python
# test_integration.py
import pytest
from product_module import add_product
from order_module import calculate_total_price

# Фикстура за настройка на тестовите данни
@pytest.fixture
def setup_products():
    add_product(1, "Laptop", 1200)
    add_product(2, "Mouse", 20)

# Тест 1: Поръчка без отстъпка
def test_order_without_discount(setup_products):
    order_items = [(2, 3)]  # 3x Mouse (20 * 3 = 60)
    total_price = calculate_total_price(order_items)
    assert total_price == 60  # Без отстъпка

# Тест 2: Поръчка с няколко продукта
def test_order_with_multiple_products(setup_products):
    order_items = [(1, 1), (2, 2)]  # 1x Laptop (1200) + 2x Mouse (20 * 2 = 40) = 1240
    total_price = calculate_total_price(order_items)
    assert total_price == 1240

# Тест 3: Поръчка с несъществуващ продукт
def test_order_with_invalid_product(setup_products):
    order_items = [(99, 1)]  # Несъществуващ продукт
    total_price = calculate_total_price(order_items)
    assert total_price == 0  # Няма такъв продукт, цената е 0
```

### Инструкции за самостоятелна работа

#### Задача: Разработка на модул за отстъпки (`discount_module.py`)

Вашата задача е да разработите модул за отстъпки, който да се интегрира в системата. Модулът трябва да прилага отстъпки върху общата цена на поръчката според следните правила:
1. Ако общата цена е над **1000**, приложи **10%** отстъпка.
2. Ако общата цена е над **500**, но под или равна на **1000**, приложи **5%** отстъпка.
3. Ако общата цена е **500** или по-малко, не прилагай отстъпка.

За целта направете fork на [приложението](https://github.com/yordan-vladov/integration-testing-example), добавете тези промени и ги запишете.
#### Стъпки за изпълнение:

1. **Създайте файл `discount_module.py`**:
    - Добавете функция `apply_discount(total_price)`, която прилага отстъпките според правилата по-горе.
2. **Интегрирайте модула в `order_module.py`**:
    - Модифицирайте функцията `calculate_total_price(order_items)`, така че да използва `apply_discount` за прилагане на отстъпки.
3. **Напишете тестове за `discount_module.py`**:
    - Създайте файл `test_discount_module.py` и напиши тестове за всички сценарии (без отстъпка, 5% отстъпка, 10% отстъпка).
4. **Актуализирайте интеграционните тестове**:
    - Добави нови тестове в `test_integration.py`, за да провериш дали отстъпките се прилагат правилно върху поръчките.

#### Инструкции за изпълнение

1. **Инсталирайте `pytest`**:
```bash
pip install pytest
```

2. **Пуснете тестовете**:
```bash
pytest # all tests
pytest test_integration.py # only integration tests
pytest test_discount_module.py # only discount unit tests
```
