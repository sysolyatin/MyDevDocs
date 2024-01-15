# Шпаргалки по С#

## Entity Framework Core Migration

```Console
Установка инструментов
dotnet tool install --global dotnet-ef

Создание первой миграции
dotnet ef migrations add InitialCreate

Обновление базы
dotnet ef database update

Развитие модели
dotnet ef migrations add AddBlogCreatedTimestamp
```

## Мелкие сниппеты

```C#
date.ToString("dd.MM.yyyy")
Request.Headers["X-Forwarded-For"].First();

// Получить русское название дня недели
CultureInfo.GetCultureInfo("ru-RU").DateTimeFormat.GetShortestDayName(DateTime.Now.DayOfWeek);
CultureInfo.GetCultureInfo("ru-RU").DateTimeFormat.GetDayName(DateTime.Now.DayOfWeek)
```
