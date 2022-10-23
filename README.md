# 4. Intro to automated functional testing

# Ссылка на копию в notion
[Lab 4](https://www.notion.so/4-Intro-to-automated-functional-testing-d99262fc75c34075b2113ecf851c2fc5)

# Обзор проекта

[Cruelty Free & Vegan Makeup | Glisten Cosmetics](https://www.glistencosmetics.com/)

Онлайн магазин декоративной косметики. Предоставляет возможность не только выбрать предлагаемые товары, но и собрать в конструкте и заказать персональный набор, выбрав количество и оттенки.

# Модуль: Корзина

## Отображение пустой корзины

**ID: 1**

**Предварительные условия:** Открыта страница корзины, в которой нет товар

|  | Шаги | Ожидаемый результат |
| --- | --- | --- |
| 1 | Просмотр страницы корзины | Отображается сообщение “Your cart is currently empty” |

**ID:** 2

**Предварительные условия:** Открыта страница корзины, в которую добавлен товар [https://www.glistencosmetics.com/products/pastel-split-liner?variant=39576325849177](https://www.glistencosmetics.com/products/pastel-split-liner?variant=39576325849177) в количестве 1

|  | Шаги | Ожидаемый результат |
| --- | --- | --- |
| 1 | Изменить в счетчике количества товара значение на 0 | Товар отображается, но его количество равно 0 |
| 2 | Нажать на кнопку пересчета стоимости товара | Товар пропал. Отображается сообщение “Your cart is currently empty” |

## Отображение товаров в корзине

**ID:** 3

**Предварительные условия:** Открыта страница корзины, в которую добавлен товар [https://www.glistencosmetics.com/products/pastel-split-liner?variant=39576325849177](https://www.glistencosmetics.com/products/pastel-split-liner?variant=39576325849177)

|  | Шаг | Ожидаемый результат |
| --- | --- | --- |
| 1 | Просмотр товара на странице корзины | Отображаются данные о добавленном товаре:</br>стоимость : £20.00</br>количество: 1</br>название : Pastel Circle (UV) Split Liner - Eyeliner - Glisten Cosmetics</br>изображение</br></br>Рядом с товаром отображается кнопка “Remove” и счетчик количества товара.</br>Видна информация об общей стоимости товаров в корзине : £20.00.</br>Отображается кнопка перезагрузки общей стоимости товаров.Доступна кнопка “Check out” |

## Подсчет общей стоимости товаров в корзине

**ID: 4**

**Описание:**

**Предварительное условие:** Открыта страница корзины, в которую добавлены один или более товаров

**Описание тестовых данных**:  Добавленные товары описаны в `initial_data`. Стоимость каждого товара и его количество описанны полями `price` и `quantity` соответственно. Ожидаемый результат описывается в `expected_result`. Массив `totals` означает стоимость товара за выбранное количество товара и относится к соответствующему товару из `initial_data`. `subtotal` описывает общую стоимость товаров в корзине 

|  | Шаг | Ожидаемый результат |
| --- | --- | --- |
| 1 | Добавить в корзину описанные тестовыми данными товары и нажать на кнопку пересчета стоимости | Отображаются данные о добавленных товарах:</br>стоимость: initial_data[n].price</br>количество initial_data[n].quantity</br>стоимость за товар: expected_result.totals[n].total</br></br>Видна информация об общей стоимости товаров в корзине: expected_result.subtotal |

```json
{
  "cases": [
    {
      "initial data": [
        {
          "price": "£20.00",
          "quantity": 2
        }
      ],
      "expected result": {
        "totals": [
          {
            "total": "£40.00"
          }
        ],
        "subtotal": "£40.00"
      }
    },
    {
      "initial data": [
        {
          "price": "£20.00",
          "quantity": 2
        },
        {
          "price": "£30.00",
          "quantity": 4
        },
        {
          "price": "£15.00",
          "quantity": 1
        }
      ],
      "expected result": {
        "totals": [
          {
            "total": "£40.00"
          },
          {
            "total": "£120.00"
          },
          {
            "total": "£15.00"
          }
        ],
        "subtotal": "£175.00"
      }
    },
    {
      "initial data": [
        {
          "price": "£3.50",
          "quantity": 3
        }
      ],
      "expected result": {
        "totals": [
          {
            "total": "£10.50"
          }
        ],
        "subtotal": "£10.50"
      }
    }
  ]
}
```

# Модуль: Оформление заказа

## Переход на страницу оформления заказа

**ID:** 5

**Предварительные условия:** Открыта страница корзины, в которую добавлен один или более товар

|  | Шаг | Ожидаемый результат |
| --- | --- | --- |
| 1 | Нажать на кнопку “Check out” | Произойдет переход на страницу уточнения деталей доставки.</br>В правой части отображаются товары из корзины, для каждого отображается:  стоимость, количество, название, изображение.</br>Видна информация об общей стоимости товаров в корзине |

## Заполнение данных формы доставки при оформлении заказа

**ID:** 6

**Предварительные условия:** Открыта страница уточнения способа доставки

|  | Шаг | Ожидаемый результат |
| --- | --- | --- |
| 1 | Ввести значения:</br>email: ivanov.ivan@gmail.com</br>first name: Ivan</br>last name:  Ivanov</br>country: Belarus</br>city: Minsk</br>address: Ivanovo 12</br>postal code: 220013</br>phone: +375291234567 | Данные без изменений отображаются в соответствующих полях. Доступна кнопка “Continue to shipping” |
| 2 | Нажать на кнопку  “Continue to shipping” | Отображаются данные, указанные на предыдущем шаге:</br>Contact: ivanov.ivan@gmail.com</br>Ship to: Ivanovo 12, 220013 Minsk, Belarus.</br></br>Отображаются список доступных вариантов доставки |
| 3 | Выбрать однин из доступных способов доставки: Tracked (Estimated shipping 7-14 business days) | Рядом с выбранным элементом списка отображается кружок |

## **Некорректное заполнение формы на** странице доставки

### Проверка заполнения обязательных полей и валидация данных:

**ID: 7**

**Предварительные условия:** Открыта страница заполнения данных клиента и доставки при оформлении заказа, состоящего из одного или более товаров

**Описание входных данных:**  Вводимые в форму данные описаны в `initial_data`. Значение `null` соответствует незаполненному полю. Ожидаемый результат описывается в `expected_result`. Поля в формате `{fieldName}_error` описывают текст ошибок для поля. `expected_result.success` со значением true описывает случай успешного заполнения формы

|  | Шаг | Ожидаемый результат |
| --- | --- | --- |
| 1 | Ввести данные из initial_data в соответствующие поля | Данные в неизменном виде отобразятся в соответствующих полях |
| 2 | Нажать на кнопку “Continue to shipping” | Сообщения из expected_result формата {fieldName}_error отобразятся под соответствующими полями.Форма не отправиться, пользователь останется на странице.

Если значение expected_result.success равно true, произойдет переход на следующий этап оформления заказа |

```json
{
  "cases": [
    {
      "initial_data": {
        "email": null,
        "country": "Belarus",
        "first_name": null,
        "last_name": null,
        "address": null,
        "postal_code": null,
        "city": null,
        "phone": null
      },
      "expected_result": {
        "email_error": "Enter an email"
      }
    },
    {
      "initial_data": {
        "email": "llsjjfdlfjs",
        "country": "Belarus",
        "first_name": null,
        "last_name": null,
        "address": null,
        "postal_code": null,
        "city": null,
        "phone": null
      },
      "expected_result": {
        "email_error": "Enter a valid email"
      }
    },
    {
      "initial_data": {
        "email": "ivan.ivanov@gmail.com",
        "country": "Belarus",
        "first_name": null,
        "last_name": null,
        "address": null,
        "postal_code": null,
        "city": null,
        "phone": null
      },
      "expected_result": {
        "first_name_error": "Enter a first name",
        "last_name_error": "Enter a last name",
        "address_error": "Enter an address",
        "city_error": "Enter a city",
        "phone_error": "Enter a phone number to use this delivery method"
      }
    },
    {
      "initial_data": {
        "email": "ivan.ivanov@gmail.com",
        "country": "Belarus",
        "first_name": "Иван",
        "last_name": "Иванов",
        "address": "Село Иваново",
        "postal_code": null,
        "city": "Минск",
        "phone": null
      },
      "expected_result": {
        "phone_error": "Enter a valid phone number"
      }
    },
    {
      "initial_data": {
        "email": "ivan.ivanov@gmail.com",
        "country": "Belarus",
        "first_name": "Ivan",
        "last_name": "Ivanov",
        "address": "Ivanovo",
        "postal_code": null,
        "city": "Minsk",
        "phone": "1"
      },
      "expected_result": {
        "success": true
      }
    },
    {
      "initial_data": {
        "email": "ivan.ivanov@gmail.com",
        "country": "Belarus",
        "first_name": "Ivan",
        "last_name": "Ivanov",
        "address": "Ivanovo",
        "postal_code": "12345678910",
        "city": "Minsk",
        "phone": "1"
      },
      "expected_result": {
        "postal_code_error": "Enter a valid ZIP / postal code for Belarus"
      }
    },
    {
      "initial_data": {
        "email": "ivan.ivanov@gmail.com",
        "country": "Belarus",
        "first_name": "Ivan",
        "last_name": "Ivanov",
        "address": "Ivanovo",
        "postal_code": null,
        "city": "Minsk",
        "phone": "1%d!!!~~l*@"
      },
      "expected_result": {
        "success": true
      }
    }
  ]
}
```

## Заполнение данных формы оплаты при оформлении заказа

**ID:** 8

**Предварительные условия:** Открыта страница уточнения способа оплаты

|  | Шаг | Ожидаемый результат |
| --- | --- | --- |
| 1 | Просмотр формы | Отображаются данные: адрес, контактная информация, способ доставки. Предлагается выбрать способ оплаты, ввести скидочный код |
| 2 | Выбрать способ оплаты “Credit card” | Откроется форма заполнения данных о карте |
| 3 | Ввести значения номера карты, держателя, срок действия, код безопасности | Информация отобразится в полях формы.</br>Доступна кнопка “Review order” |

# Модуль: Конструктор палетки

### Создание палетки

**ID:** 9

**Описание:** Открыта страница конструктора палетки подводок для глаз

|  | Шаг | Ожидаемый результат |
| --- | --- | --- |
| 1 | Просмотр страницы | Отображаются варианты выбора размера палетки и фраза “Pick Your Palette Size”. Панель выбора цветов отображается, но выделяется серым и не доступна. |
| 2 | Выбрать размер палетки 4pan | Отображается палетка нужного размера 2 на 2, панель выбора цветов активна |
| 3 | Нажать на цвет в панели выбора цветов | Цвет отобразиться в палетке |
| 4 | Заполнить все слоты в палетке цветами повторив шаг 3 еще три раза | Под формой появиться кнопка “Purchase Custom Palette” |
| 5 | Нажать на кнопку “Purchase Custom Palette” | Произойдет переход на страницу корзины, в которую добавится  составленная палетка  |

# Модуль: Поиск

## Поиск с пустым результатом

**ID:** 10

|  | Шаг | Ожидаемый результат |
| --- | --- | --- |
| 1 | Ввести в форму поиска данные:</br>1. запрос, содержащий кирриллические буквы</br>2. запрос, содержащий специальные символы</br>3. запрос из случайных латинских букв</br>4. пробелы | Запрос отображается в поисковой строке |
| 2 | Нажать клавишу “Enter” или на кнопку поиска | Результаты поиска пустые. Отображается фраза: “Your search for {search query} did not yield any results.” |

# Модуль: Карточка товара

## Добавление товара в корзину

**ID:** 11

**Предварительные условия:** Открыта страница товара [https://www.glistencosmetics.com/collections/palettes/products/pastel-split-liner](https://www.glistencosmetics.com/collections/palettes/products/pastel-split-liner). Выбрано количество товаров: 1

|  | Шаг | Ожидаемый результат |
| --- | --- | --- |
| 1 | Нажать на кнопку “Add to cart” | После непродолжительноой загрузки, сопровождаемой круговым спинером, под кнопкой появится сообщение “Item added to cart!” и текст кнопки измениться на “View cart” |