# Tournament_maker
<!DOCTYPE html>
<html>
<head>
    <title>Tournament Viewer</title>
    <style>
        body { background: #0d1117; color: white; font-family: sans-serif; text-align: center; }
        .card { background: #161b22; margin: 10px; padding: 20px; border-radius: 10px; display: inline-block; width: 300px; }
        .accent { color: #1fb1a2; }
    </style>
</head>
<body>
    <h1 id="title">Loading Tournament...</h1>
    <div id="standings"></div>

    <script>
        // Get the ID from the URL (e.g., index.html?id=jzizhah)
        const params = new URLSearchParams(window.location.search);
        const tID = params.get('id') || 'jzizhah'; 

        async function loadData() {
            const response = await fetch(`https://tournament-maker-8ca0a-default-rtdb.firebaseio.com/tournaments/${tID}.json`);
            const data = await response.json();
            
            document.getElementById('title').innerText = "🏆 " + data.name;
            
            let html = "<h2>Standings</h2>";
            Object.entries(data.scores).forEach(([team, pts]) => {
                html += `<div class="card"><b class="accent">${team}</b>: ${pts} PTS</div><br>`;
            });
            document.getElementById('standings').innerHTML = html;
        }
        loadData();
    </script>
</body>
</html>
