<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Agentforce Floating Chat</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 40px;
            text-align: center;
            background: #f9f9f9;
        }
        h1 {
            color: #2c3e50;
        }
    </style>
</head>
<body>

<h1>Agentforce Chat</h1>
<p>The floating chat icon appears in the bottom-right corner. Hidden pre-chat email is automatically set.</p>

<script type='text/javascript'>
	function initEmbeddedMessaging() {
		try {
			embeddedservice_bootstrap.settings.language = 'en_US'; // Choose your language

			embeddedservice_bootstrap.init(
				'00DgK000008l5fZ', // Org ID
				'Messaging_Channel_for_External_Website', // Deployment Name
				'https://orgfarm-de8616b37d-dev-ed.develop.my.site.com/ESWMessagingChannelfor1759308457540', // Site URL
				{
					scrt2URL: 'https://orgfarm-de8616b37d-dev-ed.develop.my.salesforce-scrt.com'
					// No widgetLocation → floating launcher icon
				}
			);
		} catch (err) {
			console.error('Error loading Embedded Messaging: ', err);
		}
	};

    // Set hidden pre-chat field after messaging is ready
    window.addEventListener("onEmbeddedMessagingReady", () => {
        console.log('Embedded Messaging is ready');

        const prechatEmail = 'contactreply@mailinator.com';
        console.log('Setting hidden pre-chat field HiddenPrechatEmail:', prechatEmail);

        if (embeddedservice_bootstrap && embeddedservice_bootstrap.prechatAPI) {
            embeddedservice_bootstrap.prechatAPI.setHiddenPrechatFields({
                'HiddenPrechatEmail': prechatEmail
            });
        } else {
            console.warn('prechatAPI not available yet');
        }
    });
</script>

<script type='text/javascript' 
    src='https://orgfarm-de8616b37d-dev-ed.develop.my.site.com/ESWMessagingChannelfor1759308457540/assets/js/bootstrap.min.js' 
    onload='initEmbeddedMessaging()'>
</script>

</body>
</html>
