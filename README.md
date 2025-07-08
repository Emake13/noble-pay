<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8"/>
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>MINI PAY PAY</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
  <style>
    /* Global styles from MINI PAY PAY code */
    body {
      font-family: 'Inter', sans-serif;
      background-color: #f1f4f9;
      margin: 0;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: flex-start; /* Align content to start for scrolling if needed */
      min-height: 100vh;
      position: relative; /* Needed for absolute positioning of app screens */
    }

    input {
      border-radius: 15px;
      border: 1px solid #ccc;
    }

    button {
      border-radius: 25px;
    }

    .hidden {
      display: none !important;
    }

    /* Common loader for MiniPay */
    .loader {
      border: 5px solid #f3f3f3;
      border-top: 5px solid #1A9C4C;
      border-radius: 50%;
      width: 40px;
      height: 40px;
      animation: spin 1s linear infinite;
      margin: 0 auto;
    }

    /* Keyframes for spin animation (used by both MiniPay and Buy PIN) */
    @keyframes spin {
      0% {
        transform: rotate(0deg);
      }
      100% {
        transform: rotate(360deg);
      }
    }

    /* --- ORIGINAL Transfer To Bank CSS (directly copied and scoped) --- */
    #transferToBankPage * {
      box-sizing: border-box;
    }

    #transferToBankPage .page { /* Original class name from your first file */
      display: none;
      min-height: 100vh;
      width: 100%;
      background-color: #f4f6f8; /* Match original body background */
      position: absolute; /* Position within #transferToBankPage */
      top: 0;
      left: 0;
      flex-direction: column; /* Allows content to stack */
      align-items: center; /* Center horizontally */
      justify-content: flex-start; /* Align header to top */
    }

    #transferToBankPage .active-page-transfer { /* New class to activate sub-pages within transfer */
      display: flex; /* Use flex to control internal layout */
    }

    #transferToBankPage .header {
      background-color: #28a745;
      color: #fff;
      padding: 16px;
      font-size: 17px;
      font-weight: 600;
      display: flex;
      align-items: center;
      width: 100%; /* Full width within its container */
      position: sticky; /* Sticky header within the page */
      top: 0;
      z-index: 20; /* Above form content */
    }

    #transferToBankPage .header .back {
      font-size: 22px;
      margin-right: 12px;
      cursor: pointer;
    }

    #transferToBankPage .container { /* Original class name, scoped to #transferToBankPage */
      padding: 20px;
      width: 100%;
      max-width: 400px; /* Constrain width to original intent */
      margin-top: 0px; /* Adjust if needed, header is sticky now */
    }

    #transferToBankPage .form-group {
      margin-bottom: 15px;
    }

    #transferToBankPage input, #transferToBankPage select {
      width: 100%;
      padding: 12px;
      font-size: 15px;
      border: 1.5px solid #28a745;
      border-radius: 8px;
      outline: none;
      height: 48px;
      background-color: #fff;
    }

    #transferToBankPage .submit-btn, #transferToBankPage .back-btn {
      width: 100%;
      background-color: #28a745;
      color: white;
      padding: 14px;
      font-size: 16px;
      border: none;
      border-radius: 8px;
      cursor: pointer;
    }

    #transferToBankPage .back-btn {
      width: auto;
      padding: 10px 14px;
      font-size: 14px;
      margin-top: 20px;
    }

    #transferToBankPage .balance {
      font-weight: bold;
      font-size: 15px;
      margin: 20px 0 25px;
    }

    #transferToBankPage .loading-page { /* Original class name, scoped */
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      height: 100vh;
      width: 100%;
      position: absolute;
      top: 0;
      left: 0;
      background-color: #f4f6f8; /* Match page background */
    }

    #transferToBankPage .loader { /* Original class name, scoped */
      border: 5px solid #f3f3f3;
      border-top: 5px solid #28a745;
      border-radius: 50%;
      width: 50px;
      height: 50px;
      animation: spin 1s linear infinite;
      margin-bottom: 20px;
    }

    #transferToBankPage .loading-page p {
      font-size: 18px;
      font-weight: bold;
      color: #333;
    }

    #transferToBankPage .success-page, #transferToBankPage .error-page { /* Original class names, scoped */
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      padding: 40px 20px;
      text-align: center;
      height: 100vh;
      width: 100%;
      position: absolute;
      top: 0;
      left: 0;
      background-color: #f4f6f8; /* Match page background */
    }

    #transferToBankPage .success-page img {
      width: 100px;
      margin-bottom: 20px;
      animation: zoomIn 0.6s ease-out;
    }

    @keyframes zoomIn {
      0% { transform: scale(0.5); opacity: 0; }
      100% { transform: scale(1); opacity: 1; }
    }

    #transferToBankPage .success-page h2 {
      color: #28a745;
      font-size: 22px;
      font-weight: bold;
      margin-bottom: 10px;
    }

    #transferToBankPage .success-page p, #transferToBankPage .error-page p {
      font-size: 15px;
      padding: 0 30px;
      margin-bottom: 20px;
    }

    #transferToBankPage .error-page h2 {
      color: #dc3545;
      font-size: 22px;
      font-weight: bold;
      margin-bottom: 10px;
    }

    #transferToBankPage .error-icon { /* Original class name, scoped */
      width: 100px;
      height: 100px;
      background-color: #dc3545;
      color: white;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 60px;
      font-weight: bold;
      margin-bottom: 20px;
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
      animation: zoomIn 0.6s ease-out;
      font-family: Arial, sans-serif;
    }
    /* --- END ORIGINAL Transfer To Bank CSS --- */

    /* Core app screen management */
    .app-screen {
      display: none; /* All app screens are hidden by default */
      width: 100%;
      max-width: 400px; /* Consistent max-width for main screens */
      box-sizing: border-box;
      position: absolute; /* Position absolutely to stack them */
      top: 0;
      left: 50%;
      transform: translateX(-50%);
      background-color: #f1f4f9; /* Default background for screens */
      z-index: 1; /* Default z-index */
      min-height: 100vh; /* Ensure screens take full viewport height */
      flex-direction: column;
      align-items: center;
      justify-content: center;
    }

    .app-screen.active-screen {
      display: flex; /* Active screen is displayed as flex */
      z-index: 10; /* Bring active screen to front */
    }

    /* Styles for the "Need Help?" text on Register/Login screens */
    .help-text-top {
      position: absolute;
      top: 1rem; /* 16px from top */
      right: 1rem; /* 16px from right */
      color: #f97316; /* Tailwind orange-500 */
      font-weight: bold;
      font-size: 0.875rem; /* Tailwind text-sm */
    }
    .help-text-top a {
        color: inherit; /* Inherit color from parent */
        text-decoration: none; /* Remove underline */
    }
    .help-text-top a:hover {
        text-decoration: underline; /* Add underline on hover for user clarity */
    }

    /* --- BUY PIN CODE SPECIFIC STYLES - MERGED HERE (SCOPED TO #buyPinScreen) --- */
    #buyPinScreen {
        font-family: 'Inter', sans-serif;
        padding-top: 2rem; /* Add some padding to the top */
        position: relative; /* For absolute positioning of header */
        overflow-x: hidden; /* Prevent horizontal scroll */
        /* background-color is controlled by JS when active */
    }
    #buyPinScreen .header {
        background-color: #2563eb; /* Blue header background */
        color: white;
        padding: 1rem 1.5rem;
        display: flex;
        align-items: center;
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        width: 100%;
        box-sizing: border-box;
        z-index: 10; /* Ensure header is above other content */
    }
    #buyPinScreen .back-arrow {
        font-size: 1.5rem;
        margin-right: 1rem;
        cursor: pointer; /* Make it clickable */
    }
    #buyPinScreen .container { /* This applies to paymentForm and bankTransferScreen */
        background-color: #ffffff;
        border-radius: 1rem; /* Rounded corners for the white card */
        box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
        width: 90%; /* Responsive width */
        max-width: 400px; /* Max width for desktop */
        padding: 1.5rem;
        margin-top: 6rem; /* Adjusted margin-top to account for fixed header */
        box-sizing: border-box; /* Include padding in width */
    }
    #buyPinScreen input[type="text"],
    #buyPinScreen input[type="email"] {
        width: 100%;
        padding: 0.75rem 1rem;
        border: 1px solid #d1d5db; /* Light gray border */
        border-radius: 0.5rem; /* Rounded corners for inputs */
        font-size: 1rem;
        color: #374151; /* Darker text color */
    }
    #buyPinScreen input::placeholder {
        color: #9ca3af; /* Placeholder color */
    }
    #buyPinScreen .label {
        font-size: 0.875rem; /* Small label text */
        font-weight: 500;
        color: #374151; /* Darker text color */
        margin-bottom: 0.5rem;
        display: block;
    }
    #buyPinScreen .button {
        background-color: #2563eb; /* Blue button */
        color: white;
        padding: 0.75rem 1.5rem;
        border-radius: 0.5rem;
        font-weight: 600;
        font-size: 1.125rem; /* Larger font size for button */
        width: 100%;
        cursor: pointer;
        transition: background-color 0.2s;
    }
    #buyPinScreen .button:hover {
        background-color: #1d4ed8; /* Darker blue on hover */
    }

    /* Loading Screen Styles */
    #buyPinScreen .loading-screen {
        display: none; /* Hidden by default */
        position: fixed; /* Cover the entire screen */
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: #2563eb; /* Same blue background as body */
        justify-content: center;
        align-items: center;
        flex-direction: column;
        z-index: 20; /* Above everything else */
    }

    #buyPinScreen .loading-card {
        background-color: #ffffff;
        border-radius: 1rem;
        box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
        width: 90%;
        max-width: 350px; /* Slightly smaller card for loading */
        padding: 2rem;
        text-align: center;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
    }

    #buyPinScreen .loading-spinner {
        width: 80px;
        height: 80px;
        border: 8px solid #e0e7ff; /* Light blue ring */
        border-top: 8px solid #2563eb; /* Blue spinning part */
        border-radius: 50%;
        animation: spin 1.5s linear infinite;
        margin-bottom: 1.5rem;
        position: relative;
    }

    #buyPinScreen .loading-spinner::before {
        content: '';
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        width: 30px; /* Size of the inner square */
        height: 30px;
        border: 2px solid #2563eb; /* Blue border for the square */
        border-radius: 0.25rem; /* Slightly rounded corners for the square */
    }

    #buyPinScreen .loading-text {
        font-size: 1.5rem;
        font-weight: 600;
        color: #1f2937; /* Dark gray text */
        margin-bottom: 0.75rem;
    }

    #buyPinScreen .loading-subtext {
        font-size: 1rem;
        color: #6b7280; /* Medium gray text */
        line-height: 1.5;
    }

    /* New styles from the user's provided HTML (Bank Transfer Screen and Overlays) */
    #buyPinScreen.bank-transfer-bg-active { /* Specific class for when the bank transfer screen is active */
        background-color: #f2f2f7; /* Light grey background from iOS */
        align-items: flex-start; /* Align to the top, as in the screenshot */
        padding-top: 0; /* No padding top for this screen */
    }

    /* Main Bank Transfer Container (Initial Screen) */
    #buyPinScreen .bank-transfer-container { /* Renamed from .container to avoid conflict */
        max-width: 400px;
        width: 100%;
        margin: 0;
        background-color: #fff;
        border-radius: 0;
        padding: 0;
        box-shadow: none;
        transition: opacity 0.3s ease-in-out, visibility 0.3s ease-in-out; /* For smooth transitions */
        z-index: 1; /* Ensure it's below overlays */
        display: none; /* Hidden by default */
        min-height: 100vh; /* Take full height */
        flex-direction: column; /* Make it a flex container for its content */
    }

    /* Styles for the top header section (Bank Transfer Screen) */
    #buyPinScreen .bt-top-header { /* Renamed from .top-header to avoid conflict */
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 15px 20px;
        background-color: #fff;
        border-bottom: 1px solid #e0e0e0;
        font-size: 17px;
        font-weight: 600;
        color: #333;
    }

    #buyPinScreen .cancel-button {
        color: #007AFF; /* iOS blue for cancel */
        font-size: 15px;
        cursor: pointer;
        font-weight: 400;
    }

    /* Styles for the main content area (Bank Transfer Screen) */
    #buyPinScreen .bt-content-area { /* Renamed from .content-area to avoid conflict */
        padding: 20px;
        background-color: #f2f2f7;
        flex-grow: 1; /* Allow content area to grow and push button to bottom */
        display: flex;
        flex-direction: column;
    }

    #buyPinScreen .amount-display {
        text-align: center;
        margin-top: 15px;
        margin-bottom: 15px;
    }

    #buyPinScreen .amount-display .main-amount {
        font-size: 28px;
        font-weight: bold;
        color: #333;
    }

    #buyPinScreen .amount-display .email {
        font-size: 14px;
        color: #666;
        margin-top: 5px;
    }

    #buyPinScreen .instruction {
        text-align: center;
        font-size: 15px;
        color: #333;
        margin: 20px 0;
    }

    #buyPinScreen .info-box {
        background-color: #fff;
        border-radius: 12px;
        padding: 15px 20px;
        margin-bottom: 20px;
        box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
    }

    #buyPinScreen .info-row {
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 10px 0;
        border-bottom: 1px solid #eee;
    }

    #buyPinScreen .info-row:last-child {
        border-bottom: none;
    }

    #buyPinScreen .info-label {
        font-size: 15px;
        color: #555;
        flex-grow: 1;
    }

    #buyPinScreen .info-value-group {
        display: flex;
        align-items: center;
    }

    #buyPinScreen .info-value {
        font-weight: 600;
        font-size: 15px;
        color: #333;
        margin-right: 10px;
    }

    #buyPinScreen .copy-button {
        background-color: #ff9500;
        color: #fff;
        border: none;
        border-radius: 6px;
        padding: 5px 12px;
        font-size: 13px;
        cursor: pointer;
        font-weight: 500;
        transition: background-color 0.2s ease;
    }

    #buyPinScreen .copy-button:active {
        background-color: #e08000;
    }

    #buyPinScreen .note {
        font-size: 14px;
        color: #666;
        line-height: 1.5;
        margin-top: 10px;
        margin-bottom: 25px;
        text-align: left;
        padding: 0 5px;
    }

    #buyPinScreen .confirm-button {
        background-color: #ff9500;
        color: white;
        font-size: 16px;
        font-weight: 600;
        border: none;
        border-radius: 10px;
        padding: 14px;
        width: calc(100% - 40px);
        margin: auto 20px 20px 20px; /* Push to bottom */
        cursor: pointer;
        transition: background-color 0.2s ease;
        -webkit-appearance: none;
    }

    #buyPinScreen .confirm-button:active {
        background-color: #e08000;
    }

    /* Adjustments for better mobile experience */
    @media (max-width: 420px) {
        #buyPinScreen .bt-content-area {
            padding: 15px;
        }

        #buyPinScreen .info-box {
            padding: 15px;
        }

        #buyPinScreen .confirm-button {
            width: calc(100% - 30px);
            margin: auto 15px 15px 15px;
        }
    }

    /* --- General Overlay Styles --- */
    #buyPinScreen .overlay {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: rgba(0, 0, 0, 0.4); /* Semi-transparent background */
        display: flex;
        justify-content: center;
        align-items: center;
        z-index: 1000;
        opacity: 0;
        visibility: hidden;
        transition: opacity 0.3s ease-in-out, visibility 0.3s ease-in-out;
    }

    #buyPinScreen .overlay.active {
        opacity: 1;
        visibility: visible;
    }

    #buyPinScreen .modal-card { /* General style for cards within overlays */
        background: white;
        border-radius: 16px;
        padding: 40px 30px;
        width: 100%;
        max-width: 320px;
        text-align: center;
        box-shadow: 0 8px 24px rgba(0, 0, 0, 0.1);
    }

    /* --- Verifying Payment Loading Overlay Styles --- */
    #buyPinScreen .spinner {
        width: 60px;
        height: 60px;
        border: 4px solid #e0e0e0; /* Light grey border */
        border-top: 4px solid #007AFF; /* Blue top border for spinning effect */
        border-radius: 50%;
        animation: spin 1s linear infinite; /* Spin animation */
        margin: 0 auto 30px; /* Center and space below spinner */
    }

    #buyPinScreen .loading-title {
        font-size: 22px;
        font-weight: 600;
        color: #333;
        margin-bottom: 10px;
    }

    #buyPinScreen .loading-message {
        font-size: 15px;
        color: #666;
        line-height: 1.5;
        margin-bottom: 5px;
    }

    #buyPinScreen .loading-sub-message {
        font-size: 13px;
        color: #888;
    }

    /* --- Payment Not Successful Overlay Styles --- */
    #buyPinScreen .error-icon-circle {
        width: 80px; /* Larger icon size */
        height: 80px;
        background-color: #FF3B30; /* Red color for error icon */
        border-radius: 50%;
        display: flex;
        justify-content: center;
        align-items: center;
        margin: 0 auto 30px; /* Center and space below icon */
        position: relative; /* For positioning pseudo-elements */
    }

    #buyPinScreen .error-icon-circle::before,
    #buyPinScreen .error-icon-circle::after {
        content: '';
        position: absolute;
        width: 4px; /* Thickness of the 'X' lines */
        height: 50px; /* Length of the 'X' lines */
        background-color: #fff; /* White 'X' */
        border-radius: 2px; /* Slightly rounded tips */
    }

    #buyPinScreen .error-icon-circle::before {
        transform: rotate(45deg);
    }

    #buyPinScreen .error-icon-circle::after {
        transform: rotate(-45deg);
    }

    /* Style for the "Try Again" button (reusing contact-support-link styles) */
    #buyPinScreen .try-again-button {
       display: block; /* Make it block to take full width */
   width: 100%;
        padding: 15px;
        background-color: #007AFF; /* iOS blue button */
        color: white;
        font-size: 16px;
        font-weight: 600;
        border: none; /* No border for this style */
        border-radius: 10px;
        cursor: pointer;
        transition: background-color 0.2s ease;
        text-decoration: none; /* Remove underline for links */
        -webkit-appearance: none; /* Remove default button styles for iOS */
        box-sizing: border-box; /* Include padding in width */
    }

    #buyPinScreen .try-again-button:active,
    #buyPinScreen .try-again-button:hover { /* Added hover for desktop */
        background-color: #0056b3;
    }

    #buyPinScreen .error-title {
        font-size: 22px;
        font-weight: 600;
        color: #FF3B30; /* Red for the title */
        margin-bottom: 10px;
    }

    #buyPinScreen .error-message-detail {
        font-size: 15px;
        color: #333;
        line-height: 1.5;
        margin-bottom: 5px;
    }

    #buyPinScreen .error-suggestion {
        font-size: 14px;
        color: #666;
        margin-bottom: 30px;
    }

    /* Custom Message Box Styles */
    #buyPinScreen .custom-message-box {
        display: none; /* Hidden by default */
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: rgba(0, 0, 0, 0.6);
        justify-content: center;
        align-items: center;
        z-index: 2000;
    }

    #buyPinScreen .custom-message-content {
        background: white;
        padding: 25px;
        border-radius: 12px;
        text-align: center;
        max-width: 300px;
        box-shadow: 0 5px 15px rgba(0,0,0,0.3);
    }

    #buyPinScreen .custom-message-content h4 {
        font-size: 1.25rem;
        font-weight: 600;
        margin-bottom: 15px;
        color: #333;
    }

    #buyPinScreen .custom-message-content p {
        font-size: 1rem;
        color: #666;
        margin-bottom: 20px;
    }

    #buyPinScreen .custom-message-content button {
        background-color: #007AFF;
        color: white;
        padding: 10px 20px;
        border-radius: 8px;
        border: none;
        cursor: pointer;
        font-size: 1rem;
        font-weight: 500;
        transition: background-color 0.2s ease;
    }

    #buyPinScreen .custom-message-content button:hover {
        background-color: #0056b3;
    }

    #buyPinScreen .email-display-text {
        font-weight: 600;
        color: #007AFF; /* Highlight the email address */
        word-break: break-all; /* Break long emails */
    }

  </style>
</head>
<body>

<div class="app-screen active-screen" id="registerScreen">
  <div class="help-text-top" id="helpTextRegister">
      <a href="https://wa.me/2349151268086?text=Hello%2C%20I%20need%20help%20with%20registration%20and%20login%20on%20MiniPay." target="_blank">Need Help?</a>
  </div>
  <div class="container w-[320px] text-center">
    <h1 class="text-3xl font-bold text-green-600 mb-2">MINI PAY</h1>
    <h3 class="text-gray-600 mb-4">Create your account</h3>
    <input type="text" id="regName" placeholder="Full Name" class="w-full p-3 mb-2 text-base"/>
    <input type="email" id="regEmail" placeholder="Email Address" class="w-full p-3 mb-2 text-base"/>
    <input type="password" id="regPassword" placeholder="Password" class="w-full p-3 mb-2 text-base"/>
    <button onclick="register()" class="bg-black text-white py-3 w-full text-base font-semibold">Register</button>
    <p class="mt-4 text-sm">Already have an account? <a onclick="showLogin()" class="text-blue-500 font-bold cursor-pointer">Login</a></p>
  </div>
</div>

<div class="app-screen" id="loginScreen">
  <div class="help-text-top" id="helpTextLogin">
      <a href="https://wa.me/2349151268086?text=Hello%2C%20I%20need%20help%20with%20registration%20and%20login%20on%20MiniPay." target="_blank">Need Help?</a>
  </div>
  <div class="container w-[320px] text-center">
    <h1 class="text-3xl font-bold text-green-600 mb-2">MINI PAY</h1>
    <h3 class="text-gray-600 mb-4">Login to your account</h3>
    <input type="email" id="loginEmail" placeholder="Email Address" class="w-full p-3 mb-2 text-base"/>
    <input type="password" id="loginPassword" placeholder="Password" class="w-full p-3 mb-2 text-base"/>
    <button onclick="login()" class="bg-black text-white py-3 w-full text-base font-semibold">Login</button>
    <p class="mt-4 text-sm">Don't have an account? <a onclick="showRegister()" class="text-blue-500 font-bold cursor-pointer">Register</a></p>
  </div>
</div>

<div class="app-screen" id="loadingDashboardScreen">
  <div class="text-center w-[320px]">
    <div class="loader mb-4"></div>
    <p class="text-gray-700 text-sm">Loading your dashboard...</p>
  </div>
</div>

<div class="app-screen" id="dashboardScreen">
  <div class="w-full max-w-md p-4">
    <header class="w-full bg-white shadow-md py-4 px-6 flex items-center justify-between rounded-b-2xl">
      <div class="flex items-center text-base font-medium text-gray-700">
        <span class="mr-2">👋</span> Welcome to MiniPay!
      </div>
      <div class="relative">
        <i class="fas fa-user-circle text-blue-500 text-3xl"></i>
      </div>
    </header>

    <div class="bg-[#1A9C4C] p-6 rounded-2xl shadow-lg mt-6 text-white">
      <div class="flex justify-between items-center mb-2">
        <span class="text-base font-medium opacity-90">Total</span>
        <span class="text-base font-medium opacity-90">NGN</span>
      </div>
      <div id="balance-amount" class="text-4xl font-bold mb-6 tracking-tight">₦0.00</div>
      <div class="flex space-x-4">
        <button id="deposit-button" class="flex-1 bg-white text-gray-700 font-semibold py-3 px-6 rounded-full shadow-md text-base transition-all duration-300">Deposit</button>
        <button id="withdraw-button" class="flex-1 bg-white text-gray-700 font-semibold py-3 px-6 rounded-full shadow-md text-base transition-all duration-300">Withdraw</button>
      </div>
    </div>

    <div class="bg-white p-6 rounded-2xl shadow-lg mt-6 grid grid-cols-3 gap-y-8 gap-x-4 text-center">
      <div class="flex flex-col items-center">
        <div class="w-16 h-16 bg-gray-100 rounded-full flex items-center justify-center mb-2 shadow-md"><i class="fas fa-sync-alt text-gray-600 text-2xl"></i></div>
        <span class="text-sm font-medium text-gray-700">Reset</span></div>
      <div class="flex flex-col items-center cursor-pointer" onclick="showAppScreen('buyPinScreen')">
        <div class="w-16 h-16 bg-gray-100 rounded-full flex items-center justify-center mb-2 shadow-md"><i class="fas fa-coins text-gray-600 text-2xl"></i></div>
        <span class="text-sm font-medium text-gray-700">Buy PIN</span>
      </div>
      <div class="flex flex-col items-center">
        <div class="w-16 h-16 bg-gray-100 rounded-full flex items-center justify-center mb-2 shadow-md"><i class="fas fa-signal text-gray-600 text-2xl"></i></div>
        <span class="text-sm font-medium text-gray-700">Airtime</span></div>
      <div class="flex flex-col items-center">
        <div class="w-16 h-16 bg-gray-100 rounded-full flex items-center justify-center mb-2 shadow-md"><i class="fas fa-id-card-alt text-gray-600 text-2xl"></i></div>
        <span class="text-sm font-medium text-gray-700">Contact</span></div>

      <div class="flex flex-col items-center">
        <a href="https://whatsapp.com/channel/0029Vb6bBLj3rZZkiptuvC20" target="_blank" rel="noopener noreferrer" class="w-16 h-16 bg-gray-100 rounded-full flex items-center justify-center mb-2 shadow-md">
          <i class="fas fa-globe text-gray-600 text-2xl"></i> </a>
        <a href="https://whatsapp.com/channel/0029Vb6bBLj3rZZkiptuvC20" target="_blank" rel="noopener noreferrer" class="text-sm font-medium text-gray-700">Group</a> </div>

      <div class="flex flex-col items-center">
        <div class="w-16 h-16 bg-gray-100 rounded-full flex items-center justify-center mb-2 shadow-md"><i class="fas fa-piggy-bank text-gray-600 text-2xl"></i></div>
        <span class="text-sm font-medium text-gray-700">Earn</span></div>
    </div>
  </div>
</div>

<div class="app-screen" id="transferToBankPage">
  <div class="page active-page-transfer" id="transferFormPage">
    <div class="header">
      <div class="back" onclick="showDashboard()">&#8592;</div>
      <div>Transfer To Bank</div>
    </div>
    <div class="container">
      <div class="form-group">
        <input id="accountName" type="text" placeholder="Account Name"/>
      </div>
      <div class="form-group">
        <input id="accountNumber" type="text" placeholder="Account Number (10 digits)" maxlength="10"/>
      </div>
      <div class="form-group">
        <select id="bank">
          <option selected disabled>Select Bank</option>
          <option>Access Bank</option>
          <option>GTBank</option>
          <option>First Bank</option>
          <option>UBA</option>
          <option>Zenith Bank</option>
          <option>VFD Microfinance Bank</option>
          <option>Wema Bank</option>
          <option>Unity Bank</option>
          <option>Jaiz Bank</option>
          <option>Lotus Bank</option>
          <option>Rubies Bank</option>
          <option>Palmpay</option>
          <option>OPay</option>
          <option>Moniepoint</option>
          <option>Sterling Bank</option>
          <option>Kuda</option>
          <option>Fidelity Bank</option>
          <option>Keystone Bank</option>
          <option>Bank</option>
          <option>Optimus Bank</option>
          <option>Stanic IBTC Bank</option>
          <option>SmartCash</option>
          <option>Raven Bank</option>
        </select>
      </div>
      <div class="form-group">
        <input id="amount" type="text" placeholder="Amount"/>
      </div>

      <div class="form-group" style="position: relative;">
        <input id="pin" type="password" placeholder="PIN Code"/>
        <span onclick="togglePIN()" style="
          position: absolute;
          right: 12px;
          top: 50%;
          transform: translateY(-50%);
          font-size: 14px;
          color: #28a745;
          cursor: pointer;
          font-weight: 600;
        " id="toggleText">Show</span>
      </div>

      <div class="balance">Available Balance: ₦180,000.00</div>
      <button class="submit-btn" onclick="submitForm()">Submit</button>
    </div>
  </div>

  <div class="page" id="transferLoadingPage">
    <div class="loading-page">
      <div class="loader"></div>
      <p>Processing withdrawal...</p>
    </div>
  </div>

  <div class="page" id="transferSuccessPage">
    <div class="success-page">
      <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/50/Yes_Check_Circle.svg/1024px-Yes_Check_Circle.svg.png" alt="Success"/>
      <h2>Transfer Successful</h2>
      <p id="successText">Your withdrawal has been completed successfully.</p>
      <button class="back-btn" onclick="goHome()">Back to Home</button>
    </div>
  </div>

  <div class="page" id="transferErrorPage">
    <div class="error-page">
      <div class="error-icon">×</div>
      <h2>Withdraw Not Successful</h2>
      <p>Check the PIN code and try again.</p>
      <button class="back-btn" onclick="goHome()">Back to Home</button>
    </div>
  </div>
</div>

<div class="app-screen" id="buyPinScreen">
    <div class="header" id="buyPinMainHeader">
        <span class="back-arrow" onclick="showDashboard()">&#8592;</span> <h1 class="text-xl font-semibold" id="buyPinHeaderTitle">Buy PIN Code</h1>
    </div>

    <div class="container" id="buyPinPaymentForm">
        <h2 class="text-xl font-semibold text-gray-800 mb-6">Complete Payment</h2>

        <div class="mb-5">
            <label for="buyPinAmount" class="label">Amount</label>
            <input type="text" id="buyPinAmount" value="₦6,500" readonly class="bg-gray-50">
        </div>

        <div class="mb-5">
            <label for="buyPinFullName" class="label">Full Name</label>
            <input type="text" id="buyPinFullName" placeholder="Your full name">
        </div>

        <div class="mb-8">
            <label for="buyPinEmailAddress" class="label">Your Email Address</label>
            <input type="email" id="buyPinEmailAddress" placeholder="email address">
        </div>

        <button class="button" id="buyPinPayButton">Pay</button>
    </div>

    <div class="loading-screen" id="buyPinInitialLoadingScreen">
        <div class="loading-card">
            <div class="loading-spinner"></div>
            <p class="loading-text">Preparing Payment Account</p>
            <p class="loading-subtext">Please wait while we set up your payment details...</p>
        </div>
    </div>

    <div class="bank-transfer-container" id="buyPinBankTransferScreen">
        <div class="bt-top-header">
            <div>Bank Transfer</div>
            <div class="cancel-button" id="buyPinBankTransferCancelBtn">Cancel</div>
        </div>

        <div class="bt-content-area">
            <div class="amount-display">
                <div class="main-amount">NGN 6,500</div>
                <div class="email">Amount to transfer</div>
            </div>
            <div class="instruction">Complete this bank transfer to proceed do not use Opay bank transfer</div>

            <div class="info-box">
                <div class="info-row">
                    <div class="info-label">Amount</div>
                    <div class="info-value-group">
                        <span class="info-value" id="buyPinAmountToCopy">₦6,500</span>
                        <button class="copy-button" data-copy-target="buyPinAmountToCopy">Copy</button>
                    </div>
                </div>

                <div class="info-row">
                    <div class="info-label">Account Number</div>
                    <div class="info-value-group">
                        <span class="info-value" id="buyPinAccountNumberToCopy">1782299316</span>
                        <button class="copy-button" data-copy-target="buyPinAccountNumberToCopy">Copy</button>
                    </div>
                </div>

                <div class="info-row">
                    <div class="info-label">Bank Name</div>
                    <div class="info-value-group">
                        <span class="info-value">Access Bank</span>
                    </div>
                </div>

                <div class="info-row">
                    <div class="info-label">Account Name</div>
                    <div class="info-value-group">
                        <span class="info-value">ONYEBUCHI JOSHUA</span>
                    </div>
                </div>
            </div> <div class="note">
                Kindly proceed with the payment for your PIN code to generate!!.
            </div>
            <button class="confirm-button" id="buyPinIHaveMadeTransferBtn">I have made this bank Transfer</button>
        </div>
    </div>

    <div class="overlay" id="buyPinVerifyingPaymentOverlay">
        <div class="modal-card">
            <div class="spinner"></div>
            <h3 class="loading-title">Verifying Payment</h3>
            <p class="loading-message">Please wait while we verify your payment...</p>
            <p class="loading-sub-message">This may take a few moments</p>
        </div>
    </div>

    <div class="overlay" id="buyPinPaymentFailedOverlay">
        <div class="modal-card">
            <div class="error-icon-circle"></div>
            <h3 class="error-title">Payment Not Successful!</h3>
            <p class="error-message-detail">Your payment could not be completed</p>
            <p class="error-suggestion">Copy Account details and try your transfer again</p>
            <button class="try-again-button" id="buyPinTryAgainButton">Try Again</button>
        </div>
    </div>

    <div class="custom-message-box" id="buyPinCustomMessageBox">
        <div class="custom-message-content">
            <h4 id="buyPinMessageBoxTitle"></h4>
            <p id="buyPinMessageBoxText"></p>
            <button id="buyPinMessageBoxCloseBtn">OK</button>
        </div>
    </div>
</div>
<script>
  // Simple in-memory user storage (for demonstration purposes)
  const users = {};
  let currentBalance = 0; // Initialize balance to 0, will be updated on login/register

  // Global function to show main app screens (register, login, dashboard, transferToBankPage, buyPinScreen)
  function showAppScreen(id) {
    document.querySelectorAll('.app-screen').forEach(screen => {
        screen.classList.remove('active-screen');
        // Reset specific styles when a screen is deactivated
        if (screen.id === 'buyPinScreen') {
            document.body.style.backgroundColor = '#f1f4f9'; // Reset to default MiniPay background
            document.body.style.paddingTop = '0'; // Reset padding
            document.body.style.alignItems = 'flex-start'; // Reset alignment
            screen.classList.remove('bank-transfer-bg-active'); // Remove specific class if active
        } else if (screen.id === 'transferToBankPage') {
            document.body.style.backgroundColor = '#f1f4f9'; // Reset to default MiniPay background
            document.body.style.paddingTop = '0'; // Reset padding
            document.body.style.alignItems = 'flex-start'; // Reset alignment
        }
    });

    document.getElementById(id).classList.add('active-screen');

    // Manage visibility of "Need Help?" text based on the active screen
    const helpTextRegister = document.getElementById('helpTextRegister');
    const helpTextLogin = document.getElementById('helpTextLogin');

    if (helpTextRegister) { // Check if element exists
      helpTextRegister.classList.add('hidden');
    }
    if (helpTextLogin) { // Check if element exists
      helpTextLogin.classList.add('hidden');
    }

    if (id === 'registerScreen' && helpTextRegister) {
      helpTextRegister.classList.remove('hidden');
    } else if (id === 'loginScreen' && helpTextLogin) {
      helpTextLogin.classList.remove('hidden');
    }

    // Specific logic for 'buyPinScreen' when it becomes active
    if (id === 'buyPinScreen') {
        document.body.style.backgroundColor = '#2563eb'; // Set the specific background for the Buy PIN flow
        document.body.style.paddingTop = '2rem'; // Set padding for the Buy PIN flow
        document.body.style.alignItems = 'flex-start'; // Align to top for initial form in Buy PIN

        // Ensure the correct sub-screen is shown within the buyPinScreen when it's activated
        buyPinShowPaymentForm(); // Call the specific function for Buy PIN flow
    } else if (id === 'dashboardScreen') {
        document.body.style.backgroundColor = '#f1f4f9'; // Reset to default dashboard background
        document.body.style.paddingTop = '0'; // Reset padding
    } else if (id === 'transferToBankPage') {
        document.body.style.backgroundColor = '#f4f6f8'; // Set specific background for Transfer flow
        document.body.style.paddingTop = '0'; // Set padding for Transfer flow
    }
  }

  // Function to show sub-pages within the Transfer To Bank flow (form, loading, success, error)
  function showTransferSubPage(id) {
    // Hide all direct children of #transferToBankPage that have the class 'page'
    document.querySelectorAll('#transferToBankPage .page').forEach(p => p.classList.remove('active-page-transfer'));
    // Display the specific sub-page
    document.getElementById(id).classList.add('active-page-transfer');
  }

  // Update the balance displayed on the dashboard and withdrawal form
  function updateBalanceDisplay() {
    document.getElementById('balance-amount').textContent = `₦${currentBalance.toLocaleString()}.00`;
    // Only update balance on the transfer form if it exists on the current page
    const balanceTransferElement = document.querySelector('#transferToBankPage .balance');
    if (balanceTransferElement) {
      balanceTransferElement.innerText = `Available Balance: ₦${currentBalance.toLocaleString()}.00`;
    }
  }

// --- Registration and Login Functions ---
  function register() {
    const name = document.getElementById("regName").value.trim();
    const email = document.getElementById("regEmail").value.trim().toLowerCase();
    const password = document.getElementById("regPassword").value;

    if (!name || !email || !password) {
      alert("Please fill all fields.");
      return;
    }

    // Email format validation: must contain '@'
    if (!email.includes('@')) {
      alert("Please enter a complete email address (e.g., example@domain.com).");
      return;
    }

    if (users[email]) {
      alert("Email already registered.");
      return;
    }

    // Assign initial balance and deposit status to new users
    users[email] = { name, password, balance: 0, hasDeposited: false }; // Start with 0, hasDeposited: false
    localStorage.setItem("loggedInUserEmail", email); // Store logged-in user email
    currentBalance = users[email].balance; // Set current balance for the new user
    showLoadingAndGoDashboard();
  }

  function login() {
    const email = document.getElementById("loginEmail").value.trim().toLowerCase();
    const password = document.getElementById("loginPassword").value;

    if (!users[email]) {
      alert("Account not found.");
      return;
    }

    if (users[email].password !== password) {
      alert("Wrong password.");
      return;
    }

    localStorage.setItem("loggedInUserEmail", email); // Store logged-in user email
    currentBalance = users[email].balance; // Set current balance for the logged-in user
    showLoadingAndGoDashboard();
  }

  function showLogin() {
    showAppScreen('loginScreen');
  }

  function showRegister() {
    showAppScreen('registerScreen');
  }

  function showLoadingAndGoDashboard() {
    showAppScreen('loadingDashboardScreen');
    setTimeout(() => {
      // Re-fetch user balance and deposit status
      const loggedInUserEmail = localStorage.getItem("loggedInUserEmail");
      if (loggedInUserEmail && users[loggedInUserEmail]) {
        currentBalance = users[loggedInUserEmail].balance;
        updateBalanceDisplay();
        // Update deposit button state based on user's deposit status
        updateDepositButtonState(users[loggedInUserEmail].hasDeposited);
      }
      showAppScreen('dashboardScreen');
    }, 4000); // 4 seconds loading for dashboard
  }

  function showDashboard() {
    showAppScreen('dashboardScreen');
    updateBalanceDisplay(); // Ensure balance is updated when returning to dashboard

    // Update deposit button state when returning to dashboard
    const loggedInUserEmail = localStorage.getItem("loggedInUserEmail");
    if (loggedInUserEmail && users[loggedInUserEmail]) {
      updateDepositButtonState(users[loggedInUserEmail].hasDeposited);
    }
  }

  // --- Withdrawal Functions (Transfer To Bank) ---
  function formatAmount(input) {
    let value = input.value.replace(/,/g, '');
    if (!isNaN(value) && value !== '') {
    input.value = parseInt(value).toLocaleString();
    }
  }

  // Add event listener for amount input formatting (specifically for the withdrawal page)
  document.getElementById('amount')?.addEventListener('input', function () {
    formatAmount(this);
  });

  function togglePIN() {
    const pinInput = document.getElementById('pin');
    const toggleText = document.getElementById('toggleText');
    if (pinInput.type === 'password') {
      pinInput.type = 'text';
      toggleText.innerText = 'Hide';
    } else {
      pinInput.type = 'password';
      toggleText.innerText = 'Show';
    }
  }

  function submitForm() {
    const account = document.getElementById('accountNumber').value;
    const amountRaw = document.getElementById('amount').value.replace(/,/g, '');
    const name = document.getElementById('accountName').value;
    const bank = document.getElementById('bank').value;
    const pin = document.getElementById('pin').value;
    const withdrawalAmount = parseInt(amountRaw);

    if (!name || account.length !== 10 || bank === "Select Bank" || !amountRaw || isNaN(withdrawalAmount) || withdrawalAmount <= 0) {
      alert("Please fill out all fields correctly.");
      return;
    }

    if (withdrawalAmount > currentBalance) {
      alert("Insufficient balance.");
      return;
    }

    // Show withdrawal loading page
    showTransferSubPage('transferLoadingPage');

    setTimeout(() => {
      if (pin !== "Minipay@2025") { // Your specified PIN code
        showTransferSubPage('transferErrorPage');
      } else {
        currentBalance -= withdrawalAmount; // Deduct from balance
        const loggedInUserEmail = localStorage.getItem("loggedInUserEmail");
        if (loggedInUserEmail && users[loggedInUserEmail]) {
          users[loggedInUserEmail].balance = currentBalance; // Update user's stored balance
        }

        const formattedAmount = withdrawalAmount.toLocaleString();
        document.getElementById('successText').innerText =
          `Your withdrawal of ₦${formattedAmount} has been completed successfully.` +
          ` Your new balance is ₦${currentBalance.toLocaleString()}.00.`; // Added new balance here for clarity
        showTransferSubPage('transferSuccessPage');
      }
      updateBalanceDisplay(); // Update balance on dashboard after withdrawal
    }, 3000); // 3 seconds loading for withdrawal
  }

  // Function to return to dashboard after withdrawal success/error
  function goHome() {
    // Clear form fields on the transfer page
    document.getElementById('accountName').value = '';
    document.getElementById('accountNumber').value = '';
    document.getElementById('bank').selectedIndex = 0;
    document.getElementById('amount').value = '';
    document.getElementById('pin').value = '';

    // Show the form page again for next time (but it will be hidden by showDashboard)
    showTransferSubPage('transferFormPage');
    showDashboard(); // Go back to dashboard
  }

  // --- Deposit Functions ---
  function updateDepositButtonState(hasDeposited) {
    const depositButton = document.getElementById('deposit-button');
    if (hasDeposited) {
      depositButton.textContent = 'Deposit Complete';
      depositButton.disabled = true;
      // Use original specific button styles from your example
      depositButton.classList.remove('bg-white', 'text-gray-700');
      depositButton.classList.add('bg-gray-300', 'text-gray-500', 'cursor-not-allowed');
    } else {
      depositButton.textContent = 'Deposit';
      depositButton.disabled = false;
      // Use original specific button styles from your example
      depositButton.classList.remove('bg-gray-300', 'text-gray-500', 'cursor-not-allowed');
      depositButton.classList.add('bg-white', 'text-gray-700');
    }
  }

  document.getElementById('deposit-button')?.addEventListener('click', () => {
    const loggedInUserEmail = localStorage.getItem("loggedInUserEmail");
    if (loggedInUserEmail && users[loggedInUserEmail] && users[loggedInUserEmail].hasDeposited) {
      alert("You have already made your one-time deposit.");
      return;
    }

    const depositAmount = 180000; // Fixed deposit amount as per your request
    currentBalance = depositAmount; // Set balance directly to 180,000

    if (loggedInUserEmail && users[loggedInUserEmail]) {
      users[loggedInUserEmail].balance = currentBalance; // Update user's stored balance
      users[loggedInUserEmail].hasDeposited = true; // Mark deposit as done for this user
    }

    updateDepositButtonState(true); // Update button state on dashboard
    updateBalanceDisplay(); // Update balance on dashboard immediately

    // Provide immediate feedback to the user via an alert with the simplified message
    alert(`Deposit of ₦${depositAmount.toLocaleString()} Deposit Successfully`);
  });

  document.getElementById('withdraw-button')?.addEventListener('click', () => {
    showAppScreen('transferToBankPage'); // Show the dedicated Transfer To Bank page
    showTransferSubPage('transferFormPage'); // Ensure the main form content is visible
    updateBalanceDisplay(); // Make sure the balance on the form is updated
  });

  // --- BUY PIN CODE JAVASCRIPT - MERGED AND SCOPED ---

    // Get references to elements for BUY PIN flow (scoped to #buyPinScreen)
    const buyPinScreen = document.getElementById('buyPinScreen');
    const buyPinPayButton = buyPinScreen.querySelector('#buyPinPayButton');
    const buyPinPaymentForm = buyPinScreen.querySelector('#buyPinPaymentForm');
    const buyPinFullNameInput = buyPinScreen.querySelector('#buyPinFullName');
    const buyPinEmailAddressInput = buyPinScreen.querySelector('#buyPinEmailAddress');
    const buyPinInitialLoadingScreen = buyPinScreen.querySelector('#buyPinInitialLoadingScreen');
    const buyPinMainHeader = buyPinScreen.querySelector('#buyPinMainHeader');
    const buyPinHeaderTitle = buyPinScreen.querySelector('#buyPinHeaderTitle');

    const buyPinBankTransferScreen = buyPinScreen.querySelector('#buyPinBankTransferScreen');
    const buyPinIHaveMadeTransferBtn = buyPinScreen.querySelector('#buyPinIHaveMadeTransferBtn');
    const buyPinBankTransferCancelBtn = buyPinScreen.querySelector('#buyPinBankTransferCancelBtn');
    const buyPinVerifyingPaymentOverlay = buyPinScreen.querySelector('#buyPinVerifyingPaymentOverlay');
    const buyPinPaymentFailedOverlay = buyPinScreen.querySelector('#buyPinPaymentFailedOverlay');
    const buyPinCopyButtons = buyPinScreen.querySelectorAll('.copy-button'); // Select copy buttons within this screen
    const buyPinTryAgainButton = buyPinScreen.querySelector('#buyPinTryAgainButton');

    const buyPinCustomMessageBox = buyPinScreen.querySelector('#buyPinCustomMessageBox');
    const buyPinMessageBoxTitle = buyPinScreen.querySelector('#buyPinMessageBoxTitle');
    const buyPinMessageBoxText = buyPinScreen.querySelector('#buyPinMessageBoxText');
    const buyPinMessageBoxCloseBtn = buyPinScreen.querySelector('#buyPinMessageBoxCloseBtn');

    // Function to show custom message box for BUY PIN flow
    function buyPinShowCustomMessage(title, message, isHtml = false) {
        buyPinMessageBoxTitle.textContent = title;
        if (isHtml) {
            buyPinMessageBoxText.innerHTML = message;
        } else {
            buyPinMessageBoxText.textContent = message;
        }
        buyPinCustomMessageBox.style.display = 'flex';
    }

    // Function to hide custom message box for BUY PIN flow
    buyPinMessageBoxCloseBtn.addEventListener('click', () => {
        buyPinCustomMessageBox.style.display = 'none';
    });

    // --- Functions to manage screen visibility within BUY PIN FLOW ---
    function buyPinHideAllContentScreens() {
        buyPinPaymentForm.style.display = 'none';
        buyPinInitialLoadingScreen.style.display = 'none';
        buyPinBankTransferScreen.style.display = 'none';
        buyPinVerifyingPaymentOverlay.classList.remove('active');
        buyPinPaymentFailedOverlay.classList.remove('active');
        buyPinCustomMessageBox.style.display = 'none'; // Ensure custom message box is hidden

        // Reset body styles to original payment form defaults or current state
        document.body.style.backgroundColor = '#2563eb';
        document.body.style.paddingTop = '2rem';
        document.body.style.alignItems = 'flex-start';
        buyPinScreen.classList.remove('bank-transfer-bg-active'); // Remove specific background class
        buyPinMainHeader.style.display = 'flex'; // Ensure header is visible by default
    }

    function buyPinShowPaymentForm() {
        buyPinHideAllContentScreens();
        buyPinPaymentForm.style.display = 'block';
        buyPinHeaderTitle.textContent = 'Buy PIN Code';
        buyPinMainHeader.style.display = 'flex'; // Ensure header is visible
        // Clear inputs when returning to form
        buyPinFullNameInput.value = '';
        buyPinEmailAddressInput.value = '';
        document.body.style.backgroundColor = '#2563eb'; // Ensure correct background
        document.body.style.paddingTop = '2rem';
        document.body.style.alignItems = 'flex-start';
    }

    function buyPinShowInitialLoadingScreen() {
        buyPinHideAllContentScreens();
        buyPinInitialLoadingScreen.style.display = 'flex';
        buyPinMainHeader.style.display = 'none'; // Hide header during initial loading
        document.body.style.backgroundColor = '#2563eb'; // Ensure correct background
        document.body.style.alignItems = 'center'; // Center loading screen vertically
        document.body.style.paddingTop = '0';
    }

    function buyPinShowBankTransferScreen() {
        buyPinHideAllContentScreens();
        buyPinBankTransferScreen.style.display = 'flex'; // Use flex to make it a flex container
        buyPinMainHeader.style.display = 'none'; // Hide the original header, as bank transfer has its own
        buyPinScreen.classList.add('bank-transfer-bg-active'); // Apply specific background class to the screen div
        document.body.style.backgroundColor = '#f2f2f7'; // Set background for this screen
        document.body.style.alignItems = 'flex-start'; // Align to top for this screen
        document.body.style.paddingTop = '0'; // No padding top for this screen
    }

    function buyPinShowVerifyingPaymentOverlay() {
        // Keep the bank transfer screen's background color (#f2f2f7) on the body
        document.body.style.backgroundColor = '#f2f2f7';
        document.body.style.alignItems = 'center'; // Center overlay vertically
        document.body.style.paddingTop = '0'; // Ensure no padding top

        buyPinBankTransferScreen.style.display = 'none'; // Hide the bank transfer screen
        buyPinMainHeader.style.display = 'none'; // Hide the "Buy PIN Code" header
        buyPinVerifyingPaymentOverlay.classList.add('active'); // Show the overlay
    }

    function buyPinShowPaymentFailedOverlay() {
        // Keep the bank transfer screen's background color (#f2f2f7) on the body
        document.body.style.backgroundColor = '#f2f2f7';
        document.body.style.alignItems = 'center'; // Center overlay vertically
        document.body.style.paddingTop = '0'; // Ensure no padding top

        buyPinBankTransferScreen.style.display = 'none'; // Hide the bank transfer screen
        buyPinMainHeader.style.display = 'none'; // Hide the "Buy PIN Code" header
        buyPinVerifyingPaymentOverlay.classList.remove('active'); // Ensure verifying overlay is hidden
        buyPinPaymentFailedOverlay.classList.add('active'); // Show the failed overlay
    }

    // --- Event Listeners for BUY PIN Flow ---

    // Handle "Pay" button click on the initial form
    buyPinPayButton.addEventListener('click', () => {
        const fullName = buyPinFullNameInput.value.trim();
        const emailAddress = buyPinEmailAddressInput.value.trim();

        // Basic validation for Full Name
        if (fullName === '') {
            buyPinShowCustomMessage('Input Error', 'Please enter your full name.');
            return; // Stop execution if validation fails
        }

        // Basic validation for Email Address
        const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
        if (emailAddress === '') {
            buyPinShowCustomMessage('Input Error', 'Please enter your email address.');
            return;
        }
        if (!emailRegex.test(emailAddress)) {
            buyPinShowCustomMessage('Input Error', 'Please enter a valid email address.');
            return;
        }

        // If all validations pass, proceed to loading screen
        buyPinShowInitialLoadingScreen();

        // Simulate initial payment processing delay (6 seconds as requested)
        setTimeout(() => {
            buyPinShowBankTransferScreen(); // Transition to the bank transfer screen
        }, 6000);
    });

    // Handle "I have made this bank Transfer" button click
    buyPinIHaveMadeTransferBtn.addEventListener('click', function() {
        buyPinShowVerifyingPaymentOverlay();

        // Simulate verification process for 5 seconds
        setTimeout(() => {
            buyPinShowPaymentFailedOverlay(); // Transition to the failed screen after 5 seconds
        }, 5000);
    });

    // Handle "Cancel" button on bank transfer screen
    buyPinBankTransferCancelBtn.addEventListener('click', function() {
        buyPinShowCustomMessage('Bank Transfer', 'Bank Transfer cancelled!');
        // After showing message, remain on the bank transfer screen
        buyPinShowBankTransferScreen();
    });

    // Handle "Try Again" button click
    buyPinTryAgainButton.addEventListener('click', function() {
        buyPinShowPaymentForm(); // Go back to the initial payment form
    });

    // --- Copy functionality for BUY PIN Flow ---
    buyPinCopyButtons.forEach(button => {
        button.addEventListener('click', function() {
            const targetId = this.getAttribute('data-copy-target');
            // Select the element *within* the buyPinScreen to ensure correct target
            const textElement = buyPinScreen.querySelector('#' + targetId);

            if (textElement) {
                let textToCopy = textElement.innerText;
                let success = false;
                try {
                    // Attempt modern Clipboard API first (might not work in all WebViews)
                    if (navigator.clipboard && navigator.clipboard.writeText) {
                        navigator.clipboard.writeText(textToCopy);
                        success = true;
                    } else {
                        // Fallback to document.execCommand (more compatible in some older WebViews/iframes)
                        const tempInput = document.createElement('textarea');
                        tempInput.value = textToCopy;
                        document.body.appendChild(tempInput);
                        tempInput.select();
                        document.execCommand('copy');
                        document.body.removeChild(tempInput);
                        success = true;
                    }
                } catch (err) {
                    console.error('Failed to copy text:', err);
                    buyPinShowCustomMessage('Copy Error', 'Failed to copy text automatically. Please copy manually: ' + textToCopy);
                    success = false;
                }

                if (success) {
                    const originalText = this.textContent;
                    this.textContent = 'Copied!';
                    setTimeout(() => {
                        this.textContent = originalText;
                    }, 1500);
                }
            }
        });
    });

  // --- Initial Load Logic ---
  window.onload = () => {
    // Check if a user is already "logged in" from a previous session
    const loggedInUserEmail = localStorage.getItem("loggedInUserEmail");
    if (loggedInUserEmail && users[loggedInUserEmail]) {
      // If a user is "logged in", load their balance and deposit status, then show the dashboard
      currentBalance = users[loggedInUserEmail].balance;
      showDashboard();
    } else {
      // Otherwise, show the registration screen
      showAppScreen('registerScreen');
    }
  };
</script>

</body>
</html>
