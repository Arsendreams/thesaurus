<!doctype html>
<html lang="en">
<head>
    <style>
    body {
        font-family: 'Georgia', serif;
        font-size: 18px;
        color: #4a4a4a;
        background-color: #faf5e6;
        background-image: url('https://example.com/yourimage.jpg'); /* Optional background image */
        background-size: cover;
        background-attachment: fixed;
        margin: 30px;
        line-height: 1.6;
    }

    h1 {
        font-size: 36px;
        color: #2e2e2e;
        text-align: center;
        font-weight: bold;
        letter-spacing: 1.2px;
    }

    input {
        padding: 10px;
        font-size: 20px;
        width: 80%;
        border: 2px solid #c5bfb6;
        border-radius: 5px;
        margin-bottom: 20px;
        background-color: #fdfdfd;
        font-family: 'Georgia', serif;
    }

    button {
        padding: 12px 25px;
        font-size: 20px;
        background-color: #4a4a4a;
        color: #fff;
        border: none;
        border-radius: 5px;
        cursor: pointer;
        transition: background-color 0.3s ease;
    }

    button:hover {
        background-color: #6d6d6d;
    }

    ul {
        list-style-type: decimal; /* Change list to numbered */
        padding: 0;
        margin-left: 40px;
    }

    li {
        font-size: 22px;
        margin: 8px 0;
        color: #2e2e2e;
        font-family: 'Palatino Linotype', 'Book Antiqua', Palatino, serif;
    }
</style>

</head><body><h1>Arsen Thesaurus</h1> <!-- Changed title -->
<input type="text" id="word-input" placeholder="Enter a word">
<button onclick="fetchThesaurus()">Search</button>

<ul id="synonyms-list"></ul> <!-- List for synonyms -->


    
    <!-- Include your JavaScript code -->
    <script>
        // Function to fetch synonyms from Datamuse API
        function fetchThesaurus() {
            let word = document.getElementById('word-input').value.trim();
            if (word === '') {
                alert('Please enter a word.');
                return;
            }
            let url = `https://api.datamuse.com/words?rel_syn=${word}`;

            fetch(url)
                .then(response => response.json())
                .then(data => {
                    let synonymList = document.getElementById('synonyms-list');
                    synonymList.innerHTML = ''; // Clear previous results

                    if (data.length === 0) {
                        let listItem = document.createElement('li');
                        listItem.textContent = 'No synonyms found.';
                        synonymList.appendChild(listItem);
                    } else {
                        data.forEach(item => {
                            let listItem = document.createElement('li');
                            listItem.textContent = item.word;
                            synonymList.appendChild(listItem);
                        });
                    }
                })
                .catch(error => {
                    console.error('Error:', error);
                    alert('An error occurred while fetching synonyms.');
                });
        }
    </script>

</body></html>
