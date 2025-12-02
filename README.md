<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>แอปเช็คชื่อนักเรียน</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    body {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: 'Sarabun', 'Noto Sans Thai', sans-serif;
      height: 100%;
      width: 100%;
    }
    
    html {
      height: 100%;
      width: 100%;
    }
    
    .app-wrapper {
      width: 100%;
      min-height: 100%;
    }
    
    .toast {
      position: fixed;
      top: 20px;
      right: 20px;
      padding: 16px 24px;
      border-radius: 8px;
      color: white;
      font-weight: 500;
      z-index: 1000;
      animation: slideIn 0.3s ease-out;
    }
    
    @keyframes slideIn {
      from {
        transform: translateX(400px);
        opacity: 0;
      }
      to {
        transform: translateX(0);
        opacity: 1;
      }
    }
    
    .loading-spinner {
      border: 3px solid rgba(255, 255, 255, 0.3);
      border-radius: 50%;
      border-top: 3px solid white;
      width: 20px;
      height: 20px;
      animation: spin 1s linear infinite;
      display: inline-block;
      margin-left: 8px;
    }
    
    @keyframes spin {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }

    .modal-overlay {
      position: fixed;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      background: rgba(0, 0, 0, 0.5);
      display: flex;
      align-items: center;
      justify-content: center;
      z-index: 2000;
    }

    .modal-content {
      background: white;
      border-radius: 16px;
      padding: 24px;
      max-width: 500px;
      width: 90%;
      max-height: 80%;
      overflow-y: auto;
    }
  </style>
</head>
<body>
  <div class="app-wrapper" style="background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);">
    <div class="container mx-auto px-4 py-8" style="max-width: 1200px;">
      <!-- Welcome Screen -->
      <div id="welcome-screen" class="text-center">
        <div class="bg-white rounded-3xl shadow-2xl p-12 mb-6 max-w-3xl mx-auto">
          <!-- Welcome Illustration -->
          <div class="mb-8">
            <svg class="mx-auto" width="280" height="280"
