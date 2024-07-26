# Шаблон dotnet приложение

1. Из проекта необходимо удалить директории `bin` и `obj`
2. Необходимо создать директорию `.template.config`
3. И в ней создать файл `template.json` с примерно следующий содержанием 

```json
{
  "$schema": "http://json.schemastore.org/template",
  "author": "Author Name",
  "classifications": [ "App"],
  "identity": "TplApp",
  "name": "TplApp",
  "shortName": "tplapp",
  "sourceName":"tplapp",
  "tags": {
    "language": "C#",
    "type": "project"
  },
  "symbols": {
    "BankName": {
        "type": "parameter",
        "description": "Введите имя проекта ещё раз сюда",
        "datatype": "text",
        "replaces": "TplApp",
        "fileRename": "TplApp",
        "defaultValue": "TplApp"
    }
  }
}
```