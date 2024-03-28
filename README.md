<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>File Upload Example</title>
</head>
<body>
  <form id="uploadForm" enctype="multipart/form-data">
    <input type="file" id="fileInput" name="file" />
    <input type="text" id="configCodeInput" name="ConfigCode" value="CF0020" placeholder="ConfigCode" />
    <button type="button" onclick="uploadFile()">Upload</button>
  </form>

  <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
  <script>
    function uploadFile() {
      const fileInput = document.getElementById('fileInput');
      const file = fileInput.files[0];
      const configCodeInput = document.getElementById('configCodeInput');

      if (!file) {
        alert('Please select a file');
        return;
      }

      const formData = new FormData();
      formData.append('files', file, file.name); // Append file with filename
      formData.append('ConfigCode', configCodeInput.value);

      axios.post('http://ws.orix.co.th:8282/api/UploadFiles', formData, {
        headers: {
          'Content-Type': 'multipart/form-data',
        },
      })
      .then(response => {
        // Handle the response
        console.log(response.data);
        // const popupMessage = `Message: ${responseData.message}\nTotal Record: ${responseData.totalRecord}\nUpload Folder: ${responseData.data[0].uploadFolder}\nFile Path: ${responseData.data[0].filePath}`;
        // alert(response.data.data[0].uploadFolder);
        // alert(response.data.message);

        const responseDataText = JSON.stringify(response.data, null, 5); // Adds indentation for better readability
        alert(responseDataText);

      })
      .catch(error => {
        // Handle errors
        // console.error(error);
        alert(error);
      });
    }
  </script>
</body>
</html>
