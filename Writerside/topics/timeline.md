# Vis Timeline

![timeline.png](timeline.png)

- Репозиторий: [https://github.com/visjs/vis-timeline/tree/master](https://github.com/visjs/vis-timeline/tree/master)
- Примеры: [https://visjs.github.io/vis-timeline/examples/timeline/](https://visjs.github.io/vis-timeline/examples/timeline/)
- Исходники и документация на случай, если их удалят с гитхаба: <resource src="vis-timeline-master.zip" />

Мой вариант конфигурации:

```Javascript
let container = document.querySelector('#visualization');
    container.innerHTML = '';
    let response = await fetch("/URL-для-получения-данных");

    if (response.ok) {
        let rawData = await response.json();
        let dataset = [];
        Array.from(rawData).forEach((dataItem) => {
            dataset.push({
                id: dataItem.Id,
                content: dataItem.Content,
                start: dataItem.StartDate,
                end: dataItem.EndDate,
                className: dataItem.TillNow ? 'till-now' : 'disband',
                info: dataItem.Info
            })
        });
        let items = new vis.DataSet(dataset);
        let options = {
            editable: false,
            start: document.querySelector("#timelineStart").value,
            end: document.querySelector("#timelineEnd").value,
            min: new Date(2024, 0, 1),
            max: new Date(new Date().setFullYear(new Date().getFullYear() + 1)),
            locale: 'ru',
            orientation: 'top',
            tooltip: {
                template: function(originalItemData) {
                    return `<span>${originalItemData.info}</span>`;
                }
            },
            loadingScreenTemplate: function() {
                return 'Получение данных...'
            }
        };
        let timeline = new vis.Timeline(container, items, options);


        // Кнопки навигации
        function move (percentage) {
            let range = timeline.getWindow();
            let interval = range.end - range.start;

            timeline.setWindow({
                start: range.start.valueOf() - interval * percentage,
                end:   range.end.valueOf()   - interval * percentage
            });
        }
        
        $("#homeBtn").click(function (){
            timeline.setWindow({
                start: document.querySelector("#timelineStart").value,
                end:   document.querySelector("#timelineEnd").value
            });
        });
        $("#zoomIn").click(function (){timeline.zoomIn( 0.2);});
        $("#zoomOut").click(function (){timeline.zoomOut( 0.2);});
        $("#moveLeft").click(function (){move( 0.2);});
        $("#moveRight").click(function (){move(-0.2);});
        


        timeline.on('click', function (properties) {
            let itemId = properties.item; // ID элемента, на который тыкнули
        });
        
    } else {
        container.innerHTML = "Ошибка получения данных: " + response.status
    }
```