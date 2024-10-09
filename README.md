<h1 style="font-family: Georgia; font-size: 36px; color: #2e2e2e; text-align: center;">Arsen Thesaurus</h1>
<input type="text" id="word-input" placeholder="Enter a word" style="padding: 10px; font-size: 20px; width: 80%;">
<button onclick="fetchThesaurus()" style="padding: 12px 25px; font-size: 20px; background-color: #4a4a4a; color: #fff; border: none; border-radius: 5px;">Search</button>

<ul id="synonyms-list" style="list-style-type: decimal; margin-left: 40px;"></ul>

<script>
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
            synonymList.innerHTML = ''; 

            if (data.length === 0) {
                let listItem = document.createElement('li');
                listItem.textContent = 'No synonyms found.';
                synonymList.appendChild(listItem);
            } else {
                data.forEach((item, index) => {
                    let listItem = document.createElement('li');
                    listItem.textContent = `${index + 1}. ${item.word}`;
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
