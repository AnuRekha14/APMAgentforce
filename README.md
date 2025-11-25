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
                embeddedservice_bootstrap.settings.language = 'en_US';

                embeddedservice_bootstrap.init(
                    '00DgK000008l5fZ',  // NEW ORG ID
                    'Messaging_Channel_for_External_Website', // NEW DEPLOYMENT NAME
                    'https://orgfarm-de8616b37d-dev-ed.develop.my.site.com/ESWMessagingChannelfor1759308457540', // NEW SITE
                    {
                        scrt2URL: 'https://orgfarm-de8616b37d-dev-ed.develop.my.salesforce-scrt.com'  // NEW SCRT
                    }
                );
            } catch (err) {
                console.error('Error loading Embedded Messaging: ', err);
            }
        }

        // Search button handler
        document.getElementById('search-button').addEventListener('click', function() {
            const query = document.getElementById('search-input').value.trim();

            if (query) {
                if (window.embeddedservice_bootstrap) {
                    console.log('User search query:', query);

                    // Opens chat
                    embeddedservice_bootstrap.openChat();
                } else {
                    alert('Chat system is still loading. Please try again.');
                }
            } else {
                alert('Please enter a search query.');
            }
        });
    </script>

    <!-- Salesforce Embedded Messaging bootstrap loader -->
    <script 
        type="text/javascript"
        src="https://orgfarm-de8616b37d-dev-ed.develop.my.site.com/ESWMessagingChannelfor1759308457540/assets/js/bootstrap.min.js"
        onload="initEmbeddedMessaging()">
    </script>

</body>
</html>
