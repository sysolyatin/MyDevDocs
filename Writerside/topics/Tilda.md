# Tilda

## Обработка формы внешним экшеном

```Javascript
var allForms = document.querySelectorAll(".js-form-proccess[data-success-url]:not([data-success-callback='t396_onSuccess']");
Array.prototype.forEach.call(allForms, function (form) {
    let formNameInput = form.querySelector('input[name="tildaspec-formname"]')
    if (formNameInput.value !== "ИМЯ_ФОРМЫ") return;
    form.action = "ВНЕШНИЙ_ЭКШЕН";
    form.classList.remove("js-form-proccess");
});
```

У формы необходимо задать имя и адрес для редиректа. Все заполненные поля формы будут отправлены постом на 
указанный в скрипте экшен.