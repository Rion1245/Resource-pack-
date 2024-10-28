# Resource-pack-<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Minecraft Resource Pack Installer</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }

        .container {
            background-color: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }

        h1 {
            margin-bottom: 20px;
        }

        label {
            display: block;
            margin-bottom: 10px;
        }

        input[type="file"] {
            padding: 10px;
            margin-bottom: 20px;
            width: 100%;
        }

        button {
            padding: 10px 20px;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }

        button:hover {
            background-color: #45a049;
        }

        .status {
            margin-top: 20px;
            font-size: 14px;
            color: green;
        }

        .error {
            color: red;
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>Upload Minecraft Resource Pack</h1>
        <form id="resourcePackForm" enctype="multipart/form-data">
            <label for="fileInput">Select Resource Pack (.zip):</label>
            <input type="file" id="fileInput" accept=".zip" required>
            <button type="submit">Upload and Install</button>
        </form>
        <div id="status" class="status"></div>
    </div>

    <script>
        document.getElementById('resourcePackForm').addEventListener('submit', function(e) {
            e.preventDefault();

            // Get the uploaded file
            var fileInput = document.getElementById('fileInput');
            var file = fileInput.files[0];

            // Ensure it's a .zip file
            if (file && file.name.endsWith('.zip')) {
                var formData = new FormData();
                formData.append('file', file);

                // Show status
                document.getElementById('status').textContent = 'Uploading resource pack...';

                // Send the file to the backend API using fetch
                fetch('https://your-server-api/upload-resource-pack', {  // Replace with your server API
                    method: 'POST',
                    body: formData
                })
                .then(response => response.json())
                .then(data => {
                    if (data.success) {
                        document.getElementById('status').textContent = 'Resource Pack uploaded and installed!';
                    } else {
                        document.getElementById('status').textContent = 'Error uploading resource pack.';
                    }
                })
                .catch(error => {
                    console.error('Error:', error);
                    document.getElementById('status').textContent = 'An error occurred during the upload.';
                });
            } else {
                alert('Please upload a valid .zip file.');
            }
        });
    </script>

</body>
</html>
