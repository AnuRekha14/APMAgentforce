<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AgentForce Search & Salesforce Chat</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin: 50px;
        }
        h1 {
            color: #2c3e50;
        }
        #search-container {
            margin-top: 20px;
        }
        #search-input {
            width: 50%;
            padding: 10px;
            font-size: 16px;
            border-radius: 5px;
            border: 1px solid #ccc;
        }
        #search-button {
            padding: 10px 20px;
            font-size: 16px;
            margin-left: 10px;
            border-radius: 5px;
            border: none;
            background-color: #0070d2;
            color: white;
            cursor: pointer;
        }
        #search-button:hover {
            background-color: #005fb2;
        }
        #message {
            margin-top: 30px;
            font-size: 18px;
            color: #555;
        }
    </style>
</head>
<body>
    <h1>Welcome to AgentForce Search</h1>
    <p id="message">Type your question or topic below and our Salesforce agents will assist you!</p>

    <div id="search-container">
        <input type="text" id="search-input" placeholder="Search something like Google...">
        <button id="search-button">Search</button>
    </div>

    <!-- Salesforce Embedded Messaging Code -->
    <script type="text/javascript">
        function initEmbeddedMessaging() {
            try {
                embeddedservice_bootstrap.settings.language = 'en_US'; // Choose your language

                embeddedservice_bootstrap.init(
                    '00DKa00000LmGlJ', // Your Salesforce Org ID
                    'SDO_Messaging_for_Web', // Messaging deployment name
                    'https://at1758534664298.my.site.com/ESWSDOMessagingforWeb1758541033355',
                    {
                        scrt2URL: 'https://at1758534664298.my.salesforce-scrt.com'
                    }
                );
            } catch (err) {
                console.error('Error loading Embedded Messaging: ', err);
            }
        }

        // Handle search input
        document.getElementById('search-button').addEventListener('click', function() {
            const query = document.getElementById('search-input').value.trim();
            if(query) {
                // Optionally, trigger the chat with the query prefilled
                if(window.embeddedservice_bootstrap) {
                    const prefilledMsg = `User search query: "${query}"`;
                    // This opens the chat window (if not already open)
                    embeddedservice_bootstrap.openChat();
                    // You can send a message to the agent automatically (if Salesforce allows)
                    console.log(prefilledMsg);
                } else {
                    alert('Chat system is not loaded yet. Please wait a moment.');
                }
            } else {
                alert('Please enter a search query.');
            }
        });
    </script>

    <!-- Salesforce Embedded Messaging bootstrap -->
    <script type="text/javascript" src="https://at1758534664298.my.site.com/ESWSDOMessagingforWeb1758541033355/assets/js/bootstrap.min.js" onload="initEmbeddedMessaging()"></script>
</body>
</html>
