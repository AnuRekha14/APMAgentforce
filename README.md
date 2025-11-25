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
            background: #f9f9f9;
        }
        h1 {
            color: #2c3e50;
        }
        #search-container {
            margin-top: 25px;
        }
        #search-input {
            width: 50%;
            padding: 12px;
            font-size: 16px;
            border-radius: 8px;
            border: 1px solid #ccc;
        }
        #search-button {
            padding: 12px 22px;
            font-size: 16px;
            margin-left: 10px;
            border-radius: 8px;
            border: none;
            background-color: #0070d2;
            color: white;
            cursor: pointer;
        }
        #search-button:hover {
            background-color: #005fb2;
        }
        #message {
            margin-top: 20px;
            font-size: 18px;
            color: #666;
        }
    </style>
</head>

<body>

    <h1>Welcome to AgentForce Search</h1>
    <p id="message">Type your question below — our Salesforce bot or agent will help!</p>

    <div id="search-container">
        <input type="text" id="search-input" placeholder="Search (like Google)...">
        <button id="search-button">Search</button>
    </div>

    <!-- Search Button Logic -->
    <script>
        document.getElementById("search-button").addEventListener("click", function () {
            const query = document.getElementById("search-input").value.trim();

            if (!query) {
                alert("Please enter a search query.");
                return;
            }

            if (window.embeddedservice_bootstrap && embeddedservice_bootstrap.utilAPI) {

                console.log("Launching Chat with query: " + query);

                // Send the search text to Salesforce bot (Conversation Context)
                embeddedservice_bootstrap.utilAPI.setConversationContext({
                    userSearch: query
                });

                // Open the Embedded Messaging widget
                embeddedservice_bootstrap.utilAPI.launchChat();

            } else {
                alert("Chat is not ready yet. Please try again in a moment.");
            }
        });
    </script>

    <!-- Salesforce Embedded Messaging Code -->
    <script type="text/javascript">
        function initEmbeddedMessaging() {
            try {
                embeddedservice_bootstrap.settings.language = 'en_US';

                embeddedservice_bootstrap.init(
                    '00DgK000008l5fZ',  // Your Org ID
                    'Messaging_Channel_for_External_Website', // Deployment Name
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

    <!-- Bootstrap Loader for Messaging Widget -->
    <script 
        type="text/javascript" 
        src="https://orgfarm-de8616b37d-dev-ed.develop.my.site.com/ESWMessagingChannelfor1759308457540/assets/js/bootstrap.min.js"
        onload="initEmbeddedMessaging()">
    </script>

</body>
</html>
