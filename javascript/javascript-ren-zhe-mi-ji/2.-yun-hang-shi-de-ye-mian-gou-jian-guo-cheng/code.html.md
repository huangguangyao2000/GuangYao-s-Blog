# code.html

```markup
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=<device-width>, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <ul id="first"></ul>
    <script>
        function addMessage(element,message){
            var messageElement = document.createElement("li");
            messageElement.textContent = message;
            element.appendChild(messageElement);
        }
        var first = document.getElementById("first");
        addMessage(first,"Page loading")
    </script>
    <ul id="second"></ul>
    <script>
        document.body.addEventListener("mousemove",function () {
            var second = document.getElementById("second");
            addMessage(second,"Event:mousemove");
        })
        document.body.addEventListener("click",function () {
            var second = document.getElementById("second");
            addMessage(second,"Event:click")            
        })
    </script>
</body>
</html>
```

