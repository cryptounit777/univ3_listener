# Ethereum Transaction Tracker

Инструмент для мониторинга транзакций Ethereum, написанный на Rust. Отслеживает и анализирует транзакции, связанные с определенным смарт-контрактом.

## Возможности

- 🔍 Мониторинг транзакций в реальном времени
- 🎯 Фильтрация транзакций по адресу контракта
- 💰 Отслеживание передачи ETH и токенов ERC20
- 📊 Сортировка транзакций по сумме
- 🔍 Подробная информация о каждой транзакции

## Предварительные требования

- Rust (последняя стабильная версия)
- Docker (опционально)
- Ключ API Infura

## Установка

1. Клонируйте репозиторий:

```bash
git clone https://github.com/your-username/ethereum-transaction-tracker
cd ethereum-transaction-tracker
```

2. Настройте переменные окружения:

```bash
export TARGET_CONTRACT_ADDRESS=0x...  # Адрес отслеживаемого контракта
```

## Использование

### Запуск локально

```bash
cargo run
```

### Запуск через Docker

```bash
docker-compose up
```

## Функциональность

### Мониторинг транзакций

Программа подключается к сети Ethereum через WebSocket Infura и отслеживает все входящие транзакции в реальном времени. Для каждой транзакции выполняется:

1. Проверка соответствия целевому адресу контракта
2. Сбор подробной информации о транзакции
3. Анализ передачи токенов (если это ERC20 транзакция)

### Информация о транзакциях

Для каждой отслеживаемой транзакции выводится:

- Базовая информация:
  - Хеш транзакции
  - Адрес отправителя
  - Адрес получателя
  - Сумма в ETH
  
- Технические детали:
  - Цена газа (Gwei)
  - Использованный газ
  - Nonce
  - Номер блока
  - Индекс транзакции
  - Chain ID

- Информация о токенах (для ERC20):
  - Адрес токена
  - Сумма передачи

### Обработка ошибок

Программа включает типизированную обработку ошибок для следующих случаев:

```rust
#[derive(Error, Debug)]
enum TrackerError {
    WebSocketConnection(WsClientError),
    TransactionRetrieval(ProviderError),
    TransactionParsing(String),
}
```

## Структура кода

Основные компоненты:

- `main()`: Точка входа и основной цикл мониторинга
- `print_transaction_info()`: Форматированный вывод информации о транзакции
- `extract_token_info()`: Извлечение информации о передаче токенов
- Обработка ошибок через `TrackerError`

## Ограничения

- Программа останавливается после сбора 5 транзакций (для демонстрации)
- Поддерживается только стандартная функция transfer ERC20 токенов

## Участие в разработке

Приветствуются pull request'ы. Для крупных изменений, пожалуйста, сначала создайте issue для обсуждения предлагаемых изменений.

## Лицензия

MIT

## Безопасность

Если вы обнаружили уязвимость безопасности, пожалуйста, отправьте email вместо создания публичного issue.
