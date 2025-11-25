<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Embedded Messaging External Page</title>
</head>
<body>
    <h1>Embedded Messaging Test Page</h1>
    <p>The chat widget will load below. Hidden pre-chat field "User_Id" is set automatically.</p>

    <!-- Container for Embedded Messaging (optional for floating widget) -->
    <div id="embeddedMessagingContainer"></div>

    <script type="text/javascript">
        function initEmbeddedMessaging() {
            try {
                embeddedservice_bootstrap.settings.language = 'en_US';

                embeddedservice_bootstrap.init(
                    '00DgK000008l5fZ', // Org ID
                    'Messaging_Channel_for_External_Website', // Deployment Name
                    'https://orgfarm-de8616b37d-dev-ed.develop.my.site.com/ESWMessagingChannelfor1759308457540', // Site URL
                    {
                        scrt2URL: 'https://orgfarm-de8616b37d-dev-ed.develop.my.salesforce-scrt.com'
                        // For in-page embed, you could add: widgetLocation: "#embeddedMessagingContainer"
                    }
                );
            } catch (err) {
                console.error('Error loading Embedded Messaging: ', err);
            }
        }

        // Listen for Embedded Messaging ready event
        window.addEventListener("onEmbeddedMessagingReady", () => {
            console.log('Inside Messaging Ready Block');

            // Set hidden pre-chat field User_Id to your provided value
            const userId = 'contactreply@mailinator.com';
            console.log('User Id:', userId);

            if (embeddedservice_bootstrap && embeddedservice_bootstrap.prechatAPI) {
                embeddedservice_bootstrap.prechatAPI.setHiddenPrechatFields({
                    'HiddenPrechatEmail': userId
                });
            } else {
                console.warn('prechatAPI not available yet');
            }
        });
    </script>

    <!-- Salesforce Embedded Messaging bootstrap -->
    <script type="text/javascript"
        src="https://orgfarm-de8616b37d-dev-ed.develop.my.site.com/ESWMessagingChannelfor1759308457540/assets/js/bootstrap.min.js"
        onload="initEmbeddedMessaging()">
    </script>
</body>
</html>
