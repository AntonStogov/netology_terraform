# Домашнее задание к занятию «Микросервисы: подходы»
### Вы работаете в крупной компании, которая строит систему на основе микросервисной архитектуры. Вам как DevOps-специалисту необходимо выдвинуть предложение по организации инфраструктуры для разработки и эксплуатации.

### Задача 1: Обеспечить разработку
#### Предложите решение для обеспечения процесса разработки: хранение исходного кода, непрерывная интеграция и непрерывная поставка. Решение может состоять из одного или нескольких программных продуктов и должно описывать способы и принципы их взаимодействия.

#### Решение должно соответствовать следующим требованиям:

#### - облачная система;
#### - система контроля версий Git;
#### - репозиторий на каждый сервис;
#### - запуск сборки по событию из системы контроля версий;
#### - запуск сборки по кнопке с указанием параметров;
#### - возможность привязать настройки к каждой сборке;
#### - возможность создания шаблонов для различных конфигураций сборок;
#### - возможность безопасного хранения секретных данных (пароли, ключи доступа);
#### - несколько конфигураций для сборки из одного репозитория;
#### - кастомные шаги при сборке;
#### - собственные докер-образы для сборки проектов;
#### - возможность развернуть агентов сборки на собственных серверах;
#### - возможность параллельного запуска нескольких сборок;
#### - возможность параллельного запуска тестов.
#### Обоснуйте свой выбор.

#### Ответ: Для ответа я подготовил сравнительную таблицу среди сервисов
```
| Возможности                            | GitLab CI/CD               | Jenkins                    | GitHub Actions            | TeamCity                
|----------------------------------------|----------------------------|----------------------------|---------------------------|-------------------------
| Облачная система                       | Да                         | Нет (локально)             | Да                        | Да                      
| Система контроля версий Git            | Встроенная                 | Интеграция                 | Встроенная                | Интеграция              
| Репозиторий на каждый сервис           | Да                         | Да                         | Да                        | Да                      
| Запуск сборки по событию               | Да                         | Да                         | Да                        | Да                      
| Запуск сборки по кнопке с параметрами  | Да                         | Да                         | Да                        | Да                      
| Настройки для каждой сборки            | Да                         | Да                         | Да                        | Да                      
| Создание шаблонов для сборок           | Да                         | Да                         | Ограничено                | Да                      
| Безопасное хранение секретных данных   | Да (встроено)              | Да (через Vault/плагины)   | Да (Secrets)              | Да                      
| Несколько конфигураций сборки          | Да                         | Да                         | Да                        | Да                      
| Кастомные шаги при сборке              | Да                         | Да                         | Да                        | Да                      
| Собственные докер-образы               | Да                         | Да                         | Да                        | Да                      
| Агенты на собственных серверах         | Да                         | Да                         | Нет                       | Да                      
| Параллельные сборки                    | Да                         | Да                         | Да                        | Да                      
| Параллельное тестирование              | Да                         | Да                         | Да                        | Да                      
```
#### Моим выбором будет GitLab CI/CD так как он предоставляет облачную систему с интегрированным контролем версий Git, поддержкой шаблонов сборок, безопасного хранения секретных данных, кастомными шагами и возможностью развертывания агентов. Это решение объединяет все необходимые функции для разработки и эксплуатации.

---

### Задача 2: Логи
#### Предложите решение для обеспечения сбора и анализа логов сервисов в микросервисной архитектуре. Решение может состоять из одного или нескольких программных продуктов и должно описывать способы и принципы их взаимодействия.

#### Решение должно соответствовать следующим требованиям:

#### - сбор логов в центральное хранилище со всех хостов, обслуживающих систему;
#### - минимальные требования к приложениям, сбор логов из stdout;
#### - гарантированная доставка логов до центрального хранилища;
#### - обеспечение поиска и фильтрации по записям логов;
#### - обеспечение пользовательского интерфейса с возможностью предоставления доступа разработчикам для поиска по записям логов;
#### - возможность дать ссылку на сохранённый поиск по записям логов.
#### Обоснуйте свой выбор.

#### Ответ: 

---

### Задача 3: Мониторинг
#### Предложите решение для обеспечения сбора и анализа состояния хостов и сервисов в микросервисной архитектуре. Решение может состоять из одного или нескольких программных продуктов и должно описывать способы и принципы их взаимодействия.

#### Решение должно соответствовать следующим требованиям:

#### - сбор метрик со всех хостов, обслуживающих систему;
#### - сбор метрик состояния ресурсов хостов: CPU, RAM, HDD, Network;
#### - сбор метрик потребляемых ресурсов для каждого сервиса: CPU, RAM, HDD, Network;
#### - сбор метрик, специфичных для каждого сервиса;
#### - пользовательский интерфейс с возможностью делать запросы и агрегировать информацию;
#### - пользовательский интерфейс с возможностью настраивать различные панели для отслеживания состояния системы.
#### Обоснуйте свой выбор.

#### Ответ:

---
