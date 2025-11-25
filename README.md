<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Agentforce Embedded Messaging</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 40px;
            text-align: center;
        }
        h1 {
            color: #2c3e50;
        }
        #embeddedMessagingContainer {
            width: 400px;
            height: 600px;
            margin: 40px auto;
            border: 1px solid #ccc;
            border-radius: 8px;
        }
    </style>
</head>
<body>

<h1>Agentforce Messaging</h1>
<p>The chat widget below is embedded and the hidden User_Id is automatically set.</p>

<!-- Optional container for in-page chat -->
<div id="embeddedMessagingContainer"></div>

<script type="text/javascript">
    function initEmbeddedMessaging() {
        try {
            embeddedservice_bootstrap.settings.language = 'en_US';

            embeddedservice_bootstrap.init(
                '00DgK000008l5fZ', // Org ID
                'New_Messaging_Channel_for_Agentforce', // Deployment Name
                'https://orgfarm-de8616b37d-dev-ed.develop.my.site.com/ESWNewMessagingChannel1756465403500', // Site URL
                {
                    scrt2URL: 'https://orgfarm-de8616b37d-dev-ed.develop.my.salesforce-scrt.com',
                    widgetLocation: '#embeddedMessagingContainer' // embeds chat in-page
                }
            );
        } catch (err) {
            console.error('Error loading Embedded Messaging: ', err);
        }
    }

    // Set hidden pre-chat field after messaging is ready
    window.addEventListener("onEmbeddedMessagingReady", () => {
        console.log('Embedded Messaging is ready');

        const userId = 'contactreply@mailinator.com';
        console.log('Setting hidden pre-chat field User_Id:', userId);

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
    src="https://orgfarm-de8616b37d-dev-ed.develop.my.site.com/ESWNewMessagingChannel1756465403500/assets/js/bootstrap.min.js"
    onload="initEmbeddedMessaging()">
</script>

</body>
</html>
