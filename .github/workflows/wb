<!DOCTYPE html>
<html lang="hu">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Boltos Játék</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: #f7f9fc;
            padding: 20px;
            color: #333;
        }
        h1 {
            text-align: center;
            color: #007bff;
            margin-bottom: 20px;
        }
        .shelf {
            border: 1px solid #ddd;
            border-radius: 10px;
            background-color: #fff;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            padding: 20px;
            margin-bottom: 20px;
            position: relative;
            transition: box-shadow 0.3s ease;
            display: flex;
            align-items: center;
        }
        .shelf:hover {
            box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
        }
        .shelf .drag-handle {
            width: 10px;
            height: 30px;
            background-color: #007bff;
            border-radius: 5px;
            cursor: move;
            margin-right: 15px;
        }
        .product-input, .image-input, .shelf-name-input {
            display: block;
            width: calc(100% - 22px);
            margin: 10px auto;
            padding: 10px;
            border-radius: 5px;
            border: 1px solid #ccc;
            font-size: 16px;
        }
        .delete-btn {
            background-color: #dc3545;
            color: #fff;
            border: none;
            padding: 8px 12px;
            cursor: pointer;
            border-radius: 5px;
            font-size: 14px;
            transition: background-color 0.3s ease;
            position: absolute;
            top: 10px;
            right: 10px;
        }
        .delete-btn:hover {
            background-color: #c82333;
        }
        .shelf img {
            width: 100px;
            height: 100px;
            object-fit: cover;
            border-radius: 5px;
            margin-top: 10px;
        }
        .add-shelf-btn, .save-btn {
            display: block;
            margin: 20px auto;
            padding: 12px 20px;
            background-color: #28a745;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            transition: background-color 0.3s ease;
        }
        .save-btn {
            background-color: #007bff;
        }
        .add-shelf-btn:hover {
            background-color: #218838;
        }
        .save-btn:hover {
            background-color: #0056b3;
        }
        .search-input {
            width: calc(100% - 22px);
            padding: 12px;
            margin: 20px auto;
            border: 1px solid #ccc;
            border-radius: 5px;
            font-size: 16px;
        }
        .search-results {
            margin-top: 20px;
        }
        .search-result {
            border: 1px solid #ddd;
            border-radius: 10px;
            background-color: #fff;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            padding: 20px;
            margin-bottom: 20px;
        }
        .search-result img {
            width: 100px;
            height: 100px;
            object-fit: cover;
            border-radius: 5px;
            margin-top: 10px;
        }
        .no-result {
            text-align: center;
            margin-top: 20px;
            color: #dc3545;
            font-size: 18px;
        }
        .confirmation-dialog {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: #fff;
            border: 1px solid #ddd;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
            padding: 20px;
            z-index: 1000;
        }
        .confirmation-dialog h2 {
            margin-top: 0;
            color: #dc3545;
        }
        .confirmation-dialog button {
            padding: 10px 15px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            margin: 5px;
        }
        .confirm-btn {
            background-color: #dc3545;
            color: #fff;
        }
        .cancel-btn {
            background-color: #6c757d;
            color: #fff;
        }
        .confirm-btn:hover {
            background-color: #c82333;
        }
        .cancel-btn:hover {
            background-color: #5a6268;
        }
        .notification {
            position: fixed;
            top: 10px;
            right: 10px;
            background-color: #28a745;
            color: #fff;
            padding: 10px 20px;
            border-radius: 5px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
            display: none;
            z-index: 1000;
            transition: opacity 0.5s ease;
        }
        .notification.show {
            display: block;
            opacity: 1;
        }
        .login-container {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        .login-form {
            background: #fff;
            border: 1px solid #ddd;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
            padding: 20px;
            width: 300px;
        }
        .login-form h2 {
            margin-top: 0;
            color: #007bff;
            text-align: center;
        }
        .login-form input {
            display: block;
            width: calc(100% - 22px);
            margin: 10px auto;
            padding: 10px;
            border-radius: 5px;
            border: 1px solid #ccc;
            font-size: 16px;
        }
        .login-form button {
            display: block;
            width: calc(100% - 22px);
            margin: 10px auto;
            padding: 10px;
            background-color: #007bff;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            transition: background-color 0.3s ease;
        }
        .login-form button:hover {
            background-color: #0056b3;
        }
    </style>
</head>
<body>
    <div id="login" class="login-container">
        <div class="login-form">
            <h2>Bejelentkezés</h2>
            <input type="password" id="password" placeholder="Jelszó">
            <button onclick="login()">Bejelentkezés</button>
        </div>
    </div>
    
    <div id="mainContent" style="display: none;">
        <h1>Boltos Játék</h1>
        
        <!-- Kereső mező -->
        <input type="text" class="search-input" id="searchBar" placeholder="Termék keresése..." oninput="searchProduct()">
        
        <!-- Keresési eredmények -->
        <div id="searchResults" class="search-results"></div>
        
        <button class="add-shelf-btn" onclick="createShelf()">Új polc létrehozása</button>
        <button class="save-btn" onclick="saveShelves()">Polcok mentése</button>
        <div id="shelves"></div>
        
        <!-- Megerősítő párbeszédablak -->
        <div id="confirmationDialog" class="confirmation-dialog">
            <h2>Biztos vagy benne, hogy törölni szeretnéd a polcot?</h2>
            <button class="confirm-btn" onclick="confirmDelete()">Igen</button>
            <button class="cancel-btn" onclick="cancelDelete()">Nem</button>
        </div>
        
        <!-- Értesítő üzenet -->
        <div id="notification" class="notification"></div>
    </div>

    <script>
        let shelfToDelete = null;

        document.addEventListener("DOMContentLoaded", () => {
            // Load shelves only if logged in
            if (sessionStorage.getItem('loggedIn')) {
                document.getElementById('login').style.display = 'none';
                document.getElementById('mainContent').style.display = 'block';
                loadShelves();
                setupSortable();
            }
        });

        function login() {
            const password = document.getElementById('password').value;
            if (password === 'BoLtReNcErEzÖ5') {
                sessionStorage.setItem('loggedIn', true);
                document.getElementById('login').style.display = 'none';
                document.getElementById('mainContent').style.display = 'block';
                loadShelves();
                setupSortable();
            } else {
                alert('Hibás jelszó!');
            }
        }

        function createShelf(shelfName = '', productName = '', productImage = '') {
            const shelves = document.getElementById('shelves');
            const shelfDiv = document.createElement('div');
            shelfDiv.className = 'shelf';

            // Drag handle
            const dragHandle = document.createElement('div');
            dragHandle.className = 'drag-handle';
            shelfDiv.appendChild(dragHandle);

            // Polc neve mező (szerkeszthető)
            const shelfNameInput = document.createElement('input');
            shelfNameInput.type = 'text';
            shelfNameInput.placeholder = 'Polc neve';
            shelfNameInput.className = 'shelf-name-input';
            shelfNameInput.value = shelfName; // Esetlegesen mentett érték
            shelfDiv.appendChild(shelfNameInput);

            // Termék neve mező
            const productNameInput = document.createElement('input');
            productNameInput.type = 'text';
            productNameInput.placeholder = 'Termék neve';
            productNameInput.className = 'product-input';
            productNameInput.value = productName; // Esetlegesen mentett érték
            shelfDiv.appendChild(productNameInput);

            // Termék képe mező
            const productImageInput = document.createElement('input');
            productImageInput.type = 'file';
            productImageInput.accept = 'image/*';
            productImageInput.className = 'image-input';
            productImageInput.onchange = function(event) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    const img = document.createElement('img');
                    img.src = e.target.result;
                    shelfDiv.appendChild(img);
                };
                reader.readAsDataURL(event.target.files[0]);
            };
            shelfDiv.appendChild(productImageInput);

            if (productImage) {
                const img = document.createElement('img');
                img.src = productImage;
                shelfDiv.appendChild(img);
            }

            // Törlés gomb hozzáadása
            const deleteButton = document.createElement('button');
            deleteButton.innerText = 'Polc törlése';
            deleteButton.className = 'delete-btn';
            deleteButton.onclick = function() {
                shelfToDelete = shelfDiv;
                document.getElementById('confirmationDialog').style.display = 'block';
            };
            shelfDiv.appendChild(deleteButton);

            shelves.appendChild(shelfDiv);
            setupSortable();
        }

        function saveShelves() {
            const shelves = document.querySelectorAll('.shelf');
            const shelfData = [];

            shelves.forEach(shelf => {
                const shelfName = shelf.querySelector('.shelf-name-input').value;
                const productName = shelf.querySelector('.product-input').value;
                const productImage = shelf.querySelector('img') ? shelf.querySelector('img').src : '';

                shelfData.push({
                    shelfName,
                    productName,
                    productImage
                });
            });

            localStorage.setItem('shelves', JSON.stringify(shelfData));
            showNotification('Polcok sikeresen elmentve!', 'success');
        }

        function loadShelves() {
            const savedShelves = JSON.parse(localStorage.getItem('shelves'));
            if (savedShelves) {
                savedShelves.forEach(shelf => {
                    createShelf(shelf.shelfName, shelf.productName, shelf.productImage);
                });
            }
        }

        function searchProduct() {
            const searchInput = document.getElementById('searchBar').value.toLowerCase();
            const shelves = JSON.parse(localStorage.getItem('shelves'));
            const searchResults = document.getElementById('searchResults');
            searchResults.innerHTML = '';

            if (!searchInput) {
                return;
            }

            let found = false;

            shelves.forEach(shelf => {
                if (shelf.productName.toLowerCase().includes(searchInput)) {
                    found = true;
                    const resultDiv = document.createElement('div');
                    resultDiv.className = 'search-result';

                    const shelfNameP = document.createElement('p');
                    shelfNameP.textContent = 'Polc neve: ' + shelf.shelfName;
                    resultDiv.appendChild(shelfNameP);

                    const productNameP = document.createElement('p');
                    productNameP.textContent = 'Termék neve: ' + shelf.productName;
                    resultDiv.appendChild(productNameP);

                    if (shelf.productImage) {
                        const img = document.createElement('img');
                        img.src = shelf.productImage;
                        resultDiv.appendChild(img);
                    }

                    searchResults.appendChild(resultDiv);
                }
            });

            if (!found) {
                const noResultDiv = document.createElement('div');
                noResultDiv.className = 'no-result';
                noResultDiv.textContent = 'Nincs találat.';
                searchResults.appendChild(noResultDiv);
            }
        }

        function confirmDelete() {
            if (shelfToDelete) {
                document.getElementById('shelves').removeChild(shelfToDelete);
                saveShelves(); // Újra mentés a törlés után
                document.getElementById('confirmationDialog').style.display = 'none';
                shelfToDelete = null;
            }
        }

        function cancelDelete() {
            document.getElementById('confirmationDialog').style.display = 'none';
            shelfToDelete = null;
        }

        function showNotification(message, type) {
            const notification = document.getElementById('notification');
            notification.textContent = message;
            notification.style.backgroundColor = type === 'success' ? '#28a745' : '#dc3545';
            notification.classList.add('show');
            setTimeout(() => {
                notification.classList.remove('show');
            }, 3000);
        }

        function setupSortable() {
            const shelves = document.getElementById('shelves');
            new Sortable(shelves, {
                handle: '.drag-handle',
                animation: 150
            });
        }
    </script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/Sortable/1.14.0/Sortable.min.js"></script>
</body>
</html>
