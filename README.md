<!DOCTYPE html>
<html lang="en">
<head>
    <style>
        /* Your CSS styles here */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        .header {
            height: 100px;
            background-color: green;
            margin: 20px;
            padding: 20px;
        }

        .container {
            height: auto;
            border: 2px solid lightgreen;
            margin: 30px;
            padding: 20px;
        }

        .ulist {
            list-style: none;
            margin: 20px;
            padding: 10px;
        }

        .list {
            border: 2px solid red;
            margin: 10px;
            padding: 5px;
            font-size: x-large;
        }

        .btn {
            margin-left: 95%;
            padding: 5px;
            font-size: x-large;
            color: white;
            background-color: red;
            text-align: center;
            display: inline;
        }

        .abc {
            border: 2px solid red;
            font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
            font-size: 20px;
        }

        .delete-button {
            margin-left: 10px;
            padding: 5px;
            font-size: large;
            background-color: #ff3333;
            color: white;
            border: none;
            cursor: pointer;
        }

        .button-container {
            display: inline-block;
            vertical-align: top;
        }
    </style>
</head>
<body>
<div class="header">
    <h1>ITEM LISTER</h1>
</div>

<div class="container">
    <h1>Add Items</h1>
    <div class="button-container">
        <input type="text" id="inp">
        <input type="button" value="Add" id="add">
        <input type="button" value="Reverse" id="reverse">
    </div>

    <ul class="ulist" id="ulists"></ul>
</div>

<script>
    let v = document.getElementById("inp");
    let addButton = document.getElementById("add");
    let reverseButton = document.getElementById("reverse");
    itemList = document.getElementById("ulists");

    // Array to store added items
    let addedItems = [];

    addButton.addEventListener('click', add);
    reverseButton.addEventListener('click', reverseOrder);

    function add() {
        let status = 1;
        let inputValue = v.value.trim();

        if (inputValue === "") {
            alert("Value is blank, You can't add this to the list");
            status = 0;
        } else if (!isNaN(inputValue)) {
            alert("Value must not be a number");
            status = 0;
        } else if (addedItems.includes(inputValue)) {
            alert("This item is already in the list.");
            status = 0;
        }

        if (status === 1) {
            let listItem = document.createElement('li');
            listItem.className = "abc";
            listItem.innerText = inputValue;

            let deleteButton = document.createElement('button');
            deleteButton.innerText = "Delete";
            deleteButton.className = "delete-button";
            deleteButton.onclick = function () {
                deleteItem(listItem);
            };

            listItem.appendChild(deleteButton);
            itemList.appendChild(listItem);

            addedItems.push(inputValue); // Add the item to the array of added items

            v.value = "";
        }
    }

    function deleteItem(item) {
        // Remove the item from the array of added items
        addedItems = addedItems.filter(itemText => itemText !== item.innerText.trim());

        itemList.removeChild(item);
    }

    function reverseOrder() {
        let listItems = Array.from(itemList.getElementsByTagName("li"));
        
        if (listItems.length === 0) {
            alert("No items to reverse.");
            return;
        }

        // Remove the last item while reversing
        let lastItem = listItems.pop();
        itemList.removeChild(lastItem);
        
        listItems.reverse();
        
        // Add the items back in reversed order
        itemList.innerHTML = '';
        listItems.forEach(function (item) {
            itemList.appendChild(item);
        });
    }
</script>
</body>
</html>
