# Шаблоны для полей модели

`Views\Shared\EditorTemplates\String.cshtml`

```html
@model string

<div class="form-floating mb-3">
    <input type="text" class="form-control" 
           id="@ViewData.ModelMetadata.PropertyName" 
           name="@ViewData.ModelMetadata.PropertyName"
           value="@ViewData.TemplateInfo.FormattedModelValue"
           placeholder="">
  <label for="@ViewData.ModelMetadata.PropertyName">@ViewData.ModelMetadata.DisplayName</label>
</div>
```

Полям в модели нужно добавить атрибут

```C#
[DisplayName("Название поля")]
```

Для вывода на вьюхе использовать консутркцию

```C#
@Html.EditorFor(a => a.FieldName)
```