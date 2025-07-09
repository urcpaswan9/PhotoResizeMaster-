<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Photo Resize Tool for Blogger</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            background-color: #f5f5f5;
            color: #333;
        }
        .container {
            background-color: white;
            border-radius: 10px;
            padding: 25px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }
        h1 {
            color: #4285f4;
            text-align: center;
            margin-bottom: 25px;
        }
        .upload-area {
            border: 2px dashed #ccc;
            border-radius: 8px;
            padding: 30px;
            text-align: center;
            margin-bottom: 20px;
            cursor: pointer;
            transition: all 0.3s;
        }
        .upload-area:hover {
            border-color: #4285f4;
            background-color: #f8faff;
        }
        .upload-area.active {
            border-color: #0f9d58;
            background-color: #e6f4ea;
        }
        #fileInput {
            display: none;
        }
        .btn {
            background-color: #4285f4;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            margin: 5px;
            transition: background-color 0.3s;
        }
        .btn:hover {
            background-color: #3367d6;
        }
        .btn-secondary {
            background-color: #f1f1f1;
            color: #333;
        }
        .btn-secondary:hover {
            background-color: #ddd;
        }
        .controls {
            margin: 20px 0;
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            align-items: center;
        }
        .control-group {
            display: flex;
            flex-direction: column;
            min-width: 150px;
        }
        label {
            margin-bottom: 5px;
            font-weight: 500;
        }
        input[type="number"], select {
            padding: 8px;
            border: 1px solid #ddd;
            border-radius: 4px;
            font-size: 16px;
        }
        .preview-container {
            display: flex;
            flex-direction: column;
            align-items: center;
            margin-top: 20px;
        }
        #preview {
            max-width: 100%;
            max-height: 400px;
            margin-bottom: 15px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        .file-info {
            margin: 10px 0;
            font-size: 14px;
            color: #666;
        }
        .quality-control {
            display: flex;
            align-items: center;
            gap: 10px;
        }
        #qualitySlider {
            flex-grow: 1;
        }
        .loading {
            display: none;
            text-align: center;
            margin: 20px 0;
        }
        .spinner {
            border: 4px solid rgba(0, 0, 0, 0.1);
            border-radius: 50%;
            border-top: 4px solid #4285f4;
            width: 30px;
            height: 30px;
            animation: spin 1s linear infinite;
            margin: 0 auto;
        }
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        .error {
            color: #d32f2f;
            margin: 10px 0;
            text-align: center;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Photo Resize Tool</h1>
        
        <div class="upload-area" id="uploadArea">
            <p><i class="icon">📁</i></p>
            <p>Drag & drop your image here or click to browse</p>
            <input type="file" id="fileInput" accept="image/jpeg, image/png, image/jpg">
            <button class="btn" id="selectBtn">Select Image</button>
        </div>
        
        <div class="file-info" id="fileInfo">No file selected</div>
        
        <div class="controls">
            <div class="control-group">
                <label for="width">Width (px)</label>
                <input type="number" id="width" placeholder="Auto" min="1">
            </div>
            
            <div class="control-group">
                <label for="height">Height (px)</label>
                <input type="number" id="height" placeholder="Auto" min="1">
            </div>
            
            <div class="control-group">
                <label for="format">Output Format</label>
                <select id="format">
                    <option value="original">Original</option>
                    <option value="jpeg">JPEG</option>
                    <option value="png">PNG</option>
                    <option value="webp">WebP</option>
                </select>
            </div>
            
            <div class="control-group" id="qualityControl" style="display:none;">
                <label for="quality">Quality</label>
                <div class="quality-control">
                    <input type="range" id="qualitySlider" min="1" max="100" value="85">
                    <span id="qualityValue">85%</span>
                </div>
            </div>
            
            <div class="control-group">
                <label>Actions</label>
                <div>
                    <button class="btn" id="resizeBtn" disabled>Resize</button>
                    <button class="btn btn-secondary" id="resetBtn">Reset</button>
                </div>
            </div>
        </div>
        
        <div class="loading" id="loading">
            <div class="spinner"></div>
            <p>Processing image...</p>
        </div>
        
        <div class="error" id="error"></div>
        
        <div class="preview-container" id="previewContainer" style="display:none;">
            <h3>Preview</h3>
            <img id="preview" src="" alt="Resized preview">
            <button class="btn" id="downloadBtn">Download Image</button>
        </div>
    </div>

    <script>
        // DOM elements
        const uploadArea = document.getElementById('uploadArea');
        const fileInput = document.getElementById('fileInput');
        const selectBtn = document.getElementById('selectBtn');
        const fileInfo = document.getElementById('fileInfo');
        const widthInput = document.getElementById('width');
        const heightInput = document.getElementById('height');
        const formatSelect = document.getElementById('format');
        const qualityControl = document.getElementById('qualityControl');
        const qualitySlider = document.getElementById('qualitySlider');
        const qualityValue = document.getElementById('qualityValue');
        const resizeBtn = document.getElementById('resizeBtn');
        const resetBtn = document.getElementById('resetBtn');
        const loading = document.getElementById('loading');
        const error = document.getElementById('error');
        const previewContainer = document.getElementById('previewContainer');
        const preview = document.getElementById('preview');
        const downloadBtn = document.getElementById('downloadBtn');
        
        // Variables
        let originalImage = null;
        let resizedImageBlob = null;
        let originalFileName = '';
        let originalFileType = '';
        
        // Event listeners
        selectBtn.addEventListener('click', () => fileInput.click());
        fileInput.addEventListener('change', handleFileSelect);
        uploadArea.addEventListener('dragover', handleDragOver);
        uploadArea.addEventListener('dragleave', handleDragLeave);
        uploadArea.addEventListener('drop', handleDrop);
        formatSelect.addEventListener('change', handleFormatChange);
        qualitySlider.addEventListener('input', updateQualityValue);
        resizeBtn.addEventListener('click', resizeImage);
        resetBtn.addEventListener('click', resetTool);
        downloadBtn.addEventListener('click', downloadImage);
        
        // Functions
        function handleFileSelect(e) {
            const file = e.target.files[0] || (e.dataTransfer && e.dataTransfer.files[0]);
            if (!file) return;
            
            if (!file.type.match('image.*')) {
                showError('Please select an image file (JPEG, PNG)');
                return;
            }
            
            processImageFile(file);
        }
        
        function handleDragOver(e) {
            e.preventDefault();
            e.stopPropagation();
            uploadArea.classList.add('active');
        }
        
        function handleDragLeave(e) {
            e.preventDefault();
            e.stopPropagation();
            uploadArea.classList.remove('active');
        }
        
        function handleDrop(e) {
            e.preventDefault();
            e.stopPropagation();
            uploadArea.classList.remove('active');
            handleFileSelect(e);
        }
        
        function handleFormatChange() {
            const format = formatSelect.value;
            qualityControl.style.display = (format === 'jpeg' || format === 'webp') ? 'block' : 'none';
        }
        
        function updateQualityValue() {
            qualityValue.textContent = `${qualitySlider.value}%`;
        }
        
        function processImageFile(file) {
            originalFileName = file.name.replace(/\.[^/.]+$/, ""); // Remove extension
            originalFileType = file.type.split('/')[1];
            
            const reader = new FileReader();
            reader.onload = function(e) {
                originalImage = new Image();
                originalImage.onload = function() {
                    fileInfo.textContent = `${file.name} (${originalImage.width}×${originalImage.height}px, ${formatBytes(file.size)})`;
                    widthInput.placeholder = originalImage.width;
                    heightInput.placeholder = originalImage.height;
                    resizeBtn.disabled = false;
                    
                    // Set default format to original
                    formatSelect.value = 'original';
                    handleFormatChange();
                };
                originalImage.src = e.target.result;
            };
            reader.readAsDataURL(file);
        }
        
        function resizeImage() {
            if (!originalImage) {
                showError('No image selected');
                return;
            }
            
            loading.style.display = 'block';
            error.textContent = '';
            previewContainer.style.display = 'none';
            
            // Get dimensions
            let width = widthInput.value ? parseInt(widthInput.value) : originalImage.width;
            let height = heightInput.value ? parseInt(heightInput.value) : originalImage.height;
            
            // Maintain aspect ratio if only one dimension is provided
            if (widthInput.value && !heightInput.value) {
                height = Math.round((width / originalImage.width) * originalImage.height);
                heightInput.value = height;
            } else if (!widthInput.value && heightInput.value) {
                width = Math.round((height / originalImage.height) * originalImage.width);
                widthInput.value = width;
            }
            
            // Create canvas
            const canvas = document.createElement('canvas');
            canvas.width = width;
            canvas.height = height;
            const ctx = canvas.getContext('2d');
            
            // Draw image on canvas
            ctx.drawImage(originalImage, 0, 0, width, height);
            
            // Process in small timeout to allow UI to update
            setTimeout(() => {
                let mimeType;
                let quality = 0.85; // Default quality
                
                // Determine output format
                const format = formatSelect.value === 'original' ? originalFileType : formatSelect.value;
                
                switch(format) {
                    case 'jpeg':
                    case 'jpg':
                        mimeType = 'image/jpeg';
                        quality = parseInt(qualitySlider.value) / 100;
                        break;
                    case 'png':
                        mimeType = 'image/png';
                        break;
                    case 'webp':
                        mimeType = 'image/webp';
                        quality = parseInt(qualitySlider.value) / 100;
                        break;
                    default:
                        mimeType = 'image/jpeg';
                }
                
                // Convert to blob
                canvas.toBlob(blob => {
                    loading.style.display = 'none';
                    
                    if (!blob) {
                        showError('Error processing image');
                        return;
                    }
                    
                    resizedImageBlob = blob;
                    preview.src = URL.createObjectURL(blob);
                    previewContainer.style.display = 'flex';
                    
                    // Update file info with new size
                    fileInfo.textContent = `${fileInfo.textContent} → Resized to ${width}×${height}px (${formatBytes(blob.size)})`;
                    
                }, mimeType, quality);
            }, 100);
        }
        
        function downloadImage() {
            if (!resizedImageBlob) return;
            
            const format = formatSelect.value === 'original' ? originalFileType : formatSelect.value;
            const extension = format === 'jpg' ? 'jpeg' : format;
            const url = URL.createObjectURL(resizedImageBlob);
            
            const a = document.createElement('a');
            a.href = url;
            a.download = `${originalFileName}_resized.${extension}`;
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            URL.revokeObjectURL(url);
        }
        
        function resetTool() {
            fileInput.value = '';
            originalImage = null;
            resizedImageBlob = null;
            fileInfo.textContent = 'No file selected';
            widthInput.value = '';
            heightInput.value = '';
            formatSelect.value = 'original';
            qualitySlider.value = '85';
            qualityValue.textContent = '85%';
            resizeBtn.disabled = true;
            loading.style.display = 'none';
            error.textContent = '';
            previewContainer.style.display = 'none';
            preview.src = '';
            handleFormatChange();
        }
        
        function showError(message) {
            error.textContent = message;
        }
        
        function formatBytes(bytes) {
            if (!bytes) return '0 Bytes';
            const k = 1024;
            const sizes = ['Bytes', 'KB', 'MB', 'GB'];
            const i = Math.floor(Math.log(bytes) / Math.log(k));
            return parseFloat((bytes / Math.pow(k, i)).toFixed(2) + ' ' + sizes[i];
        }
    </script>
</body>
</html>
