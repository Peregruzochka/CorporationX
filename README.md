# CorporationX
Это проект над которым я работал вместе со своей командой из 7 человек. Писали проект на микросервисной архитектуре. Т.к. над проектом работали разные команды, то для изучения всего кода моей команды необходимо смотреть сервисы в ветке kraken-master-stream6. Фичи реализованные мной будут указаны ниже. В ссылках отображены ключевые моменты.

# My features
## 1. Постановка целей
Реализация основныx операции: создать новую цель, обновить цель, удалить цель, получить все подзадачи цели по фильтру и получить список целей с фильтрами.
- [GoalController.java](https://github.com/CorporationX/user_service/blob/feature-BJS2-26821/src/main/java/school/faang/user_service/controller/goal/GoalController.java)
- [GoalService.java](https://github.com/CorporationX/user_service/blob/feature-BJS2-26821/src/main/java/school/faang/user_service/service/goal/GoalService.java)

## 2. Приоритет поиска для премиум-пользователей
Реализация системы приоритетного отображения аккаунтов пользователей с премиальной подпиской в поисковой выдаче, что увеличивает их видимость и потенциальные шансы на сотрудничество по сравнению с обычными пользователями.
- [UserController.java](https://github.com/CorporationX/user_service/blob/feature-BJS2-26827/src/main/java/school/faang/user_service/controller/user/UserController.java)
- [UserService.java](https://github.com/CorporationX/user_service/blob/feature-BJS2-26827/src/main/java/school/faang/user_service/service/user/UserService.java)
- [UserRepository.java](https://github.com/CorporationX/user_service/blob/feature-BJS2-26827/src/main/java/school/faang/user_service/repository/UserRepository.java)

## 3. Система видимости альбомов
В приложении можно создавать альбомы постов. Реализована полльзовательская настройка видимости для каждого альбома. Т.е. альбом, созданный определенным пользователем может быть доступен:
- Всем пользователям
- Только его подписчикам
- Только выбранным автором пользователям
- Только автору

[AlbumService.java](https://github.com/CorporationX/post_service/blob/feature-BJS2-26857/src/main/java/faang/school/postservice/service/AlbumService.java)

## 4. Добавление картинок к посту
Реализован функционал добавления посту до 10 картинок. Файлы загружаются в Minio (через Amazon S3 API), в базе данных PostgreSQL сохраняется только их ID для поиска в хранилище. Ограничение на размер файла — 5 МБ. При необходимости изображения сжимаются пропорционально наибольшей стороне до 1080px. Предусмотрена возможность редактирования поста с добавлением и удалением изображений. Возможность добавления видео и аудиофайлов была рассмотрена и реализована дополнительно.
- [MinioImageManager.java](https://github.com/CorporationX/post_service/blob/feature-BJS2-26871/src/main/java/faang/school/postservice/service/resource/minio/MinioImageManager.java)
- [ResourceService.java](https://github.com/CorporationX/post_service/blob/feature-BJS2-26871src/main/java/faang/school/postservice/service/resource/ResourceService.java)

## 5. AI орфография
Реализован функционал поддержки AI для написания постов. Пользователи могут передать текст поста AI-сервису, который автоматически проверяет его на орфографические и пунктуационные ошибки, исправляя их. Это улучшает качество текста и упрощает процесс создания постов.
- [YandexSpellerConfig.java](https://github.com/CorporationX/post_service/blob/feature-BJS2-26888/src/main/java/faang/school/postservice/config/YandexSpellerConfig.java)
- [YandexSpeller.java](https://github.com/CorporationX/post_service/blob/feature-BJS2-26888/src/main/java/faang/school/postservice/service/tools/YandexSpeller.java)

## 6. Cервис аналитики
### 6.1 Сохранение и  запрос аналитики
Реализовано сохранение events в основную БД и эндпоинт /analytics для получения аналитики любого типа
- [AnalyticsEventsController.java](https://github.com/CorporationX/analytics_service/blob/feature-BJS2-26909/src/main/java/faang/school/analytics/controller/AnalyticsEventsController.java)
- [AnalyticsEventService.java](https://github.com/CorporationX/analytics_service/blob/feature-BJS2-26909/src/main/java/faang/school/analytics/service/AnalyticsEventService.java)
- [AnalyticsEventRepository.java](https://github.com/CorporationX/analytics_service/blob/feature-BJS2-26909/src/main/java/faang/school/analytics/repository/AnalyticsEventRepository.java)

### 6.2 Анализ комментариев
Реализован сбор информации о публикации пользователями комментариев на основе отправки events в микросервис аналитики
- [CommentEventListener.java](https://github.com/CorporationX/analytics_service/blob/feature-BJS2-26914/src/main/java/faang/school/analytics/listener/CommentEventListener.java)

## 7. Получение достижения "Писатель"
В системе реализована фича "Получение достижения Писатель", которая выдается пользователю за то что он опубликовал 100 постов
- [PostEventPublishAspect.java](https://github.com/CorporationX/post_service/blob/feature-BJS2-26928/src/main/java/faang/school/postservice/publis/aspect/post/PostEventPublishAspect.java)
- [PostService.java](https://github.com/CorporationX/post_service/blob/feature-BJS2-26928/src/main/java/faang/school/postservice/service/PostService.java)
- [PostEventListener.java](https://github.com/CorporationX/achievement_service/blob/feature-BJS2-26928/src/main/java/faang/school/achievement/listener/PostEventListener.java)
- [WriterAchievementHandler.java](https://github.com/CorporationX/achievement_service/blob/feature-BJS2-26928/src/main/java/faang/school/achievement/handler/WriterAchievementHandler.java)
- [AchievementService.java](https://github.com/CorporationX/achievement_service/blob/feature-BJS2-26928/src/main/java/faang/school/achievement/service/AchievementService.java)

## 8. Создание платежного счета
Реализован функционал формирования платежных счетов в микросервисе account_service. Каждый пользователь и проект могут иметь несколько личных платежных счетов, которые используются для совершения платежей. Это обеспечивает гибкость и удобство в управлении финансами.
- [AccountController.java](https://github.com/CorporationX/account_service/blob/feature-BJS2-26951/src/main/java/faang/school/accountservice/controller/AccountController.java)
- [AccountService.java](https://github.com/CorporationX/account_service/blob/feature-BJS2-26951/src/main/java/faang/school/accountservice/service/AccountService.java)
- [AccountRepository.java](https://github.com/CorporationX/account_service/blob/feature-BJS2-26951/src/main/java/faang/school/accountservice/repository/AccountRepository.java)
- Entity [Account.java](https://github.com/CorporationX/account_service/blob/feature-BJS2-26951/src/main/java/faang/school/accountservice/model/account/Account.java)

## 9. URL Shortener
Реализация killer-feature URL Shortner
*URL Shortener — это сервис, который преобразует длинные веб-адреса (URL) в более короткие ссылки. Такие короткие ссылки легче делиться, запоминать и использовать, особенно в местах с ограничением символов (например, в соцсетях). При переходе по короткой ссылке пользователь автоматически перенаправляется на исходный длинный URL.*
![391228807-2ce45862-4b09-49cf-9112-409788374bc6](https://github.com/user-attachments/assets/a4176413-0e76-44be-8365-40eebfddf75c)
Реализован функционал для URL Shortener со следующими возможностями:
- **Генерация списка хэшей:** Создание уникальных хэшей, которые будут использоваться для формирования коротких ссылок.
- **Кэширование свободных хэшей:** При запуске микросервиса и достижении минимального порога свободных хэшей в кэше пополнять его.
- **Возврат оригинальной ссылки:** Позволяет получить исходный URL по короткому хэшу.
- **Создание короткой ссылки:** Сопоставление оригинального URL с сгенерированным хэшем и сохранение его в базе данных.
- **Редирект:** Обеспечение перенаправления пользователя с короткой ссылки на оригинальный URL.

- [UrlController.java](https://github.com/CorporationX/url_shortener_service/blob/peregruzochka-url-shortener-BJS2-42946/src/main/java/faang/school/urlshortenerservice/controller/UrlController.java)
- [UrlService.java](https://github.com/CorporationX/url_shortener_service/blob/peregruzochka-url-shortener-BJS2-42946/src/main/java/faang/school/urlshortenerservice/service/UrlService.java)
- кэширование длинных ссылок [UrlCacheRepository.java](https://github.com/CorporationX/url_shortener_service/blob/peregruzochka-url-shortener-BJS2-42946/src/main/java/faang/school/urlshortenerservice/repository/UrlCacheRepository.java)
- [Base62Encoder.java](https://github.com/CorporationX/url_shortener_service/blob/peregruzochka-url-shortener-BJS2-42946/src/main/java/faang/school/urlshortenerservice/hash/Base62Encoder.java)
- [HashCacheFiller.java](https://github.com/CorporationX/url_shortener_service/blob/peregruzochka-url-shortener-BJS2-42946/src/main/java/faang/school/urlshortenerservice/hash/HashCacheFiller.java)

## 10. News Feed
Реализация killer-feature News Fead
*News Feed - фича которая включает в себя формирования ленты новостей, для каждого пользователя*

- **Формирование ленты постов в Redis:** Лента постов каждого пользователя должна сохраняться в кэше Redis для быстрого доступа и повышения производительности.
- **Обработка конкурентного доступа:** Использование Optimistic Lock для управления конкурентным доступом к данным в Redis и предотвращения коллизий при обновлении.
- **Интеграция с Kafka:** Подключение к Kafka для обработки событий (публикация постов, комментарии, просмотры, лайки) и формирования ленты на основе этих данных.
- **Разогреватель фида:** Реализация механизма предварительной генерации ленты (news feed) для всех пользователей при первом запуске приложения.
- **Эндпоинты для получения постов:** Создание API для получения пачек постов из пользовательской ленты, соответствующих текущему состоянию news feed.

- [AbstractKafkaProducer.java](https://github.com/CorporationX/post_service/blob/news-feed-team2-developer/src/main/java/faang/school/postservice/producer/AbstractKafkaProducer.java) [KafkaPostProducer.java](https://github.com/CorporationX/post_service/blob/news-feed-team2-developer/src/main/java/faang/school/postservice/producer/KafkaPostProducer.java)
- [KafkaPostPublishConsumer.java](https://github.com/CorporationX/post_service/blob/news-feed-team2-developer/src/main/java/faang/school/postservice/listener/KafkaPostPublishConsumer.java)
- [NewsFeedRedisRepository.java](https://github.com/CorporationX/post_service/blob/news-feed-team2-developer/src/main/java/faang/school/postservice/repository/NewsFeedRedisRepository.java) [RedisTransactionRetryWrapper.java](https://github.com/CorporationX/post_service/blob/news-feed-team2-developer/src/main/java/faang/school/postservice/repository/RedisTransactionRetryWrapper.java)
- [NewsFeedController.java](https://github.com/CorporationX/post_service/blob/news-feed-team2-developer/src/main/java/faang/school/postservice/controller/NewsFeedController.java) [NewsFeedService.java](https://github.com/CorporationX/post_service/blob/news-feed-team2-developer/src/main/java/faang/school/postservice/service/NewsFeedService.java)


