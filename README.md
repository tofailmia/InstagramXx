<!DOCTYPE html>
<html>
<head>
    <title>Instagram Video Downloader with Telegram</title>
    <style>
        body { 
            font-family: Arial, sans-serif; 
            max-width: 800px; 
            margin: 0 auto; 
            padding: 20px; 
        }
        .container { 
            background: #f5f5f5; 
            padding: 20px; 
            border-radius: 8px; 
        }
        input, button { 
            padding: 10px; 
            margin: 5px 0; 
        }
        button { 
            background: #0088cc; 
            color: white; 
            border: none; 
            cursor: pointer; 
        }
    </style>
</head>

<body>
    <div class="container">
        <h1>Instagram Video Downloader</h1>
        <p>Enter Instagram URL to download video and send via Telegram</p>

        <input type="text" id="instaUrl" placeholder="https://www.instagram.com/p/..." style="width: 100%;">
        <button onclick="downloadAndSend()">Download & Send via Telegram</button>

        <div id="result" style="margin-top: 20px;"></div>
    </div>

    <script>
        async function downloadAndSend() {
            const url = document.getElementById('instaUrl').value;
            const resultDiv = document.getElementById('result');

            if (!url.includes('instagram.com')) {
                resultDiv.innerHTML = '<p style="color:red;">Please enter a valid Instagram URL</p>';
                return;
            }

            resultDiv.innerHTML = '<p>Processing...</p>';

            try {
                // In a real implementation, you would call your backend service here
                // This is just a frontend demo
                const telegramBotLink = generateTelegramBotLink(url);

                resultDiv.innerHTML = `
                    <p>Video processed successfully!</p>
                    <p><a href="${telegramBotLink}" target="_blank">Click here to send via Telegram</a></p>
                    <p>Or add this bot to your group and send the Instagram URL directly.</p>
                `;
            } catch (error) {
                resultDiv.innerHTML = `<p style="color:red;">Error: ${error.message}</p>`;
            }
        }

        function generateTelegramBotLink(instaUrl) {
            // This would be your actual bot username
            const botUsername = 'YourDownloaderBot';

            // URL encode the Instagram URL
            const encodedUrl = encodeURIComponent(instaUrl);

            return `https://t.me/${botUsername}?start=dl_${encodedUrl}`;
        }
    </script>
</body>
</html>
