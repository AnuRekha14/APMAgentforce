<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AgentForce Search + Salesforce Messaging</title>

    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin: 40px;
        }
        h1 {
            color: #2c3e50;
            margin-bottom: 10px;
        }
        #search-container {
            margin-top: 20px;
        }
        #search-input {
            width: 60%;
            padding: 12px;
            font-size: 18px;
            border-radius: 8px;
            border: 1px solid #bbb;
        }
        #search-button {
            padding: 12px 22px;
            font-size: 18px;
            margin-left: 10px;
            border-radius: 8px;
            border: none;
            background-color: #0070d2;
            color: white;
            cursor: pointer;
        }
        #search-button:hover {
            background-color: #005bb2;
        }
        #results {
            margin-top: 40px;
            text-align: left;
            max-width: 800px;
            margin-left: auto;
            margin-right: auto;
            font-size: 17px;
        }
        .result-card {
            padding: 15px;
            border-radius: 8px;
            border: 1px solid #ddd;
            margin-bottom: 20px;
            background: #fafafa;
        }
        .result-card h3 {
            margin-top: 0;
        }
    </style>
</head>

<body>

    <h1>AgentForce Search</h1>
    <p>Ask anything — Agentforce will find the answer for you!</p>

    <div id="search-container">
        <input id="search-input" type="text" placeholder="Search just like Google...">
        <button id="search-button">Search</button>
    </div>

    <div id="results"></div>

    <!-- Agentforce Search Integration -->
    <script>
        document.getElementById('search-button').addEventListener('click', async function () {
            const query = document.getElementById('search-input').value.trim();

            if (!query) {
                alert('Please enter a search query.');
                return;
            }

            document.getElementById('results').innerHTML = "<p><em>Searching Agentforce...</em></p>";

            try {
                // ⭐ IMPORTANT: Replace this endpoint with your real Agentforce Search API URL
                const response = await fetch('/agentforce/search', {
                    method: 'POST',
                    headers: { "Content-Type": "application/json" },
                    body: JSON.stringify({ query })
                });

                const data = await response.json();

                if (!data.results || data.results.length === 0) {
                    document.getElementById('results').innerHTML = "<p>No results found.</p>";
                    return;
                }

                let html = "<h2>AI Search Results</h2>";

                data.results.forEach(result => {
                    html += `
                        <div class="result-card">
                            <h3>${result.title}</h3>
                            <p>${result.summary}</p>
                        </div>
                    `;
                });

                document.getElementById('results').innerHTML = html;

            } catch (error) {
                console.error(error);
                document.getElementById('results').innerHTML =
                    "<p style='color:red;'>Error fetching search results.</p>";
            }
        });
    </script>

    <!-- Salesforce Embedded Messaging (Chat Icon) -->
    <script type='text/javascript'>
        function initEmbeddedMessaging() {
            try {
                embeddedservice_bootstrap.settings.language = 'en_US';

                embeddedservice_bootstrap.init(
                    '00DgK000008l5fZ',  
                    'Messaging_Channel_for_External_Website',
                    'https://orgfarm-de8616b37d-dev-ed.develop.my.site.com/ESWMessagingChannelfor1759308457540',
                    {
                        scrt2URL: 'https://orgfarm-de8616b37d-dev-ed.develop.my.salesforce-scrt.com'
                    }
                );
            } catch (err) {
                console.error('Error loading Embedded Messaging: ', err);
            }
        }
    </script>

    <script type='text/javascript'
        src='https://orgfarm-de8616b37d-dev-ed.develop.my.site.com/ESWMessagingChannelfor1759308457540/assets/js/bootstrap.min.js'
        onload='initEmbeddedMessaging()'>
    </script>

</body>
</html>
