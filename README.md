<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Green App Dashboard</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
        /* Base styles for the main dashboard and login screens */
        body {
            font-family: 'Inter', sans-serif;
            -webkit-font-smoothing: antialiased;
            -moz-osx-font-smoothing: grayscale;
            background-color: #f3f4f6;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 1rem;
        }

        /* Container for the main app view, with responsive width */
        .app-container {
            max-width: 420px;
            width: 100%;
            transition: opacity 0.5s ease-in-out;
            /* This is for the dashboard view to fit the screen better */
            min-height: 100vh;
            /* To make sure it takes full height when in dashboard mode */
            position: relative;
        }

        /* The Bank Withdraw screen needs to fill the entire body, so it's styled separately */
        #screen-bank-withdraw,
        #screen-data {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            display: none;
            flex-direction: column;
            background: #f0f2f5;
        }

        /* Styles from the original dashboard code to maintain the exact look */
        .icon-container {
            width: 3rem;
            height: 3rem;
            display: flex;
            align-items: center;
            justify-content: center;
            border-width: 2px;
            border-color: #22C55E;
            border-radius: 0.75rem;
            color: #22C55E;
        }

        /* Typing effect specific styles */
        .important-info-card {
            background: linear-gradient(to right, #22C55E, #10B981);
            border-radius: 1rem;
            padding: 1.25rem;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }

        .info-steps-card {
            background: linear-gradient(to right, #4ade80, #34d399);
            border-radius: 0.75rem;
            padding: 1rem;
        }

        .step-number-circle {
            width: 1.5rem;
            height: 1.5rem;
            border-radius: 9999px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 0.75rem;
            font-weight: bold;
            flex-shrink: 0;
        }

        /* Loading spinner animation */
        @keyframes spin {
            to {
                transform: rotate(360deg);
            }
        }

        .spinner {
            border: 4px solid rgba(255, 255, 255, 0.3);
            border-top: 4px solid #fff;
            border-radius: 50%;
            width: 24px;
            height: 24px;
            animation: spin 1s linear infinite;
        }

        /* === Bank Withdraw Specific CSS === */
        #screen-bank-withdraw .header {
            background: #16a34a;
            color: white;
            font-weight: bold;
            font-size: 18px;
            padding: 15px;
            display: flex;
            align-items: center;
            height: 55px;
            box-sizing: border-box;
            font-family: Arial, sans-serif;
            z-index: 10;
        }

        #screen-bank-withdraw .header-title {
            margin-left: 10px;
        }

        #screen-bank-withdraw .back-arrow {
            font-size: 22px;
            cursor: pointer;
        }

        #screen-bank-withdraw .content-container {
            padding: 20px;
            flex-grow: 1;
            /* Allow the content to take up the remaining space */
            overflow-y: auto;
            /* Enable scrolling if content overflows */
        }

        #screen-bank-withdraw h2.page-title {
            font-size: 22px;
            font-weight: bold;
            margin-bottom: 25px;
            color: #333;
            margin-top: 10px;
        }

        #screen-bank-withdraw .form-control {
            width: 100%;
            height: 55px;
            padding: 0 15px;
            margin-bottom: 18px;
            border: 1px solid #ddd;
            border-radius: 12px;
            font-size: 17px;
            background: #fff;
            appearance: none;
            outline: none;
            box-sizing: border-box;
            color: #333;
        }

        #screen-bank-withdraw .form-control::placeholder {
            color: #888;
        }

        #screen-bank-withdraw select.form-control {
            color: #888;
        }

        #screen-bank-withdraw select.form-control:focus:not([value=""]) {
            color: #333;
        }

        #screen-bank-withdraw .info-row {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 30px;
            padding: 0 5px;
        }

        #screen-bank-withdraw .available-balance {
            font-size: 15px;
            color: black;
        }

        #screen-bank-withdraw .buy-code a {
            font-size: 15px;
            color: black;
            text-decoration: none;
            font-weight: bold;
        }

        #screen-bank-withdraw .btn {
            width: 100%;
            height: 55px;
            border: none;
            border-radius: 12px;
            font-size: 18px;
            font-weight: bold;
            background: #16a34a;
            color: white;
            cursor: pointer;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }

        #screen-bank-withdraw .btn:hover {
            background: #138f3c;
        }

        #screen-bank-withdraw .btn:active {
            transform: translateY(1px);
        }

        #screen-bank-withdraw .overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: #f0f2f5;
            display: none;
            /* Changed to none for default */
            flex-direction: column;
            align-items: center;
            justify-content: center;
            z-index: 1000;
            text-align: center;
            opacity: 0;
            visibility: hidden;
            transition: opacity 0.3s ease-in-out, visibility 0.3s ease-in-out;
            padding: 20px;
            box-sizing: border-box;
        }

        #screen-bank-withdraw .overlay.visible {
            opacity: 1;
            visibility: visible;
            display: flex;
        }

        #screen-bank-withdraw #loading-overlay {
            background-color: #ffffff;
        }

        #screen-bank-withdraw .spinner-container {
            position: relative;
            width: 100px;
            height: 100px;
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        #screen-bank-withdraw .spinner-outer {
            width: 100px;
            height: 100px;
            border: 8px solid #e0e0e0;
            border-top-color: #16a34a;
            border-radius: 50%;
            animation: spin 1.2s cubic-bezier(0.5, 0.2, 0.5, 0.8) infinite;
            position: absolute;
        }

        #screen-bank-withdraw .spinner-inner {
            width: 60px;
            height: 60px;
            background-color: #16a34a;
            border-radius: 50%;
            position: absolute;
        }

        #screen-bank-withdraw .loading-text {
            font-size: 20px;
            font-weight: bold;
            color: #333;
            margin-bottom: 8px;
        }

        #screen-bank-withdraw .sub-text {
            font-size: 16px;
            color: #888;
            font-weight: normal;
        }

        #screen-bank-withdraw #success-overlay .success-icon-container {
            width: 100px;
            height: 100px;
            background-color: #e6f7e9;
            border-radius: 50%;
            display: grid;
            place-items: center;
            margin-bottom: 30px;
        }

        #screen-bank-withdraw #success-overlay .success-icon {
            width: 80px;
            height: 80px;
            background-color: #16a34a;
            border-radius: 50%;
            display: grid;
            place-items: center;
        }

        #screen-bank-withdraw #success-overlay .success-icon svg {
            width: 45px;
            height: 45px;
            color: #fff;
            stroke-width: 3;
        }

        #screen-bank-withdraw #success-overlay .status-title {
            font-size: 28px;
            font-weight: bold;
            margin-bottom: 25px;
            color: #333;
        }

        #screen-bank-withdraw #success-overlay .success-message-text {
            font-size: 18px;
            color: #333;
            line-height: 1.5;
            margin-bottom: 40px;
            padding: 0 20px;
            font-weight: normal;
        }

        #screen-bank-withdraw #success-overlay #done-btn {
            width: 90%;
            max-width: 300px;
            height: 55px;
            border-radius: 12px;
        }

        #screen-bank-withdraw .error-message {
            color: red;
            font-size: 14px;
            margin-top: -10px;
            margin-bottom: 10px;
            display: none;
            text-align: left;
            padding-left: 14px;
        }

        /* === Data Screen Specific CSS === */
        #screen-data .header {
            background: #28c34d;
            color: #fff;
            padding: 15px;
            font-size: 18px;
            font-weight: bold;
            display: flex;
            align-items: center;
        }

        #screen-data .back-btn {
            margin-right: 10px;
            font-size: 20px;
            cursor: pointer;
        }

        #screen-data .form-container {
            padding: 20px;
        }

        #screen-data .form-group {
            margin-bottom: 15px;
        }

        #screen-data select,
        #screen-data input {
            width: 100%;
            padding: 12px;
            font-size: 16px;
            border: 1px solid #ccc;
            border-radius: 8px;
            outline: none;
            box-sizing: border-box;
        }

        #screen-data .btn {
            width: 100%;
            background: #28c34d;
            color: #fff;
            border: none;
            padding: 14px;
            font-size: 18px;
            font-weight: bold;
            border-radius: 8px;
            cursor: pointer;
        }

        #screen-data .btn:hover {
            background: #22a840;
        }

        #screen-data .error {
            display: none;
            margin-top: 10px;
            padding: 10px;
            background: #e74c3c;
            color: white;
            border-radius: 6px;
            text-align: center;
            font-size: 14px;
        }

 /* Modal Success Popup */
        #screen-data .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
            justify-content: center;
            align-items: center;
            z-index: 9999;
        }

        #screen-data .modal-content {
            background: #fff;
            border-radius: 15px;
            text-align: center;
            padding: 25px 20px;
            width: 85%;
            max-width: 350px;
            animation: popup 0.3s ease-in-out;
        }

        @keyframes popup {
            from {
                transform: scale(0.8);
                opacity: 0;
            }

            to {
                transform: scale(1);
                opacity: 1;
            }
        }

        #screen-data .modal-content h2 {
            color: #28c34d;
            margin-bottom: 10px;
        }

        #screen-data .modal-content p {
            font-size: 16px;
            color: #333;
            margin-bottom: 20px;
        }

        #screen-data .ok-btn {
            background: #28c34d;
            color: #fff;
            border: none;
            padding: 12px 30px;
            font-size: 16px;
            font-weight: bold;
            border-radius: 25px;
            cursor: pointer;
        }
    </style>
</head>

<body>
    <div id="main-app" class="app-container">

        <div id="screen-signup" class="space-y-6">
            <div class="flex flex-col items-center space-y-4">
                <div class="h-16 w-16 flex items-center justify-center rounded-2xl bg-green-600 shadow-md">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-10 w-10 text-white" viewBox="0 0 24 24" fill="currentColor">
                        <path d="M13 14H19L11 21V16H6L13 9V14Z" />
                        <path d="M12 2H5V9L12 16V11H18L11 4V9H5L12 2Z" fill="white" />
                    </svg>
                </div>
                <h1 class="text-3xl font-bold text-green-900">Sign Up</h1>
                <p class="text-gray-500 text-sm">Create an account to continue.</p>
            </div>

            <form id="signup-form" class="space-y-4">
                <div>
                    <label for="full-name" class="block text-sm font-medium text-gray-700">Full Name</label>
                    <div class="mt-1">
                        <input type="text" id="full-name" name="full-name" required class="block w-full px-4 py-3 rounded-lg border-2 border-green-200 placeholder-green-300 focus:outline-none focus:ring-2 focus:ring-green-500 focus:border-transparent transition-all duration-300">
                    </div>
                </div>
                <div>
                    <label for="email" class="block text-sm font-medium text-gray-700">Email</label>
                    <div class="mt-1">
                        <input type="email" id="email" name="email" required class="block w-full px-4 py-3 rounded-lg border-2 border-green-200 placeholder-green-300 focus:outline-none focus:ring-2 focus:ring-green-500 focus:border-transparent transition-all duration-300">
                    </div>
                </div>
                <div>
                    <label for="password" class="block text-sm font-medium text-gray-700">Password</label>
                    <div class="mt-1">
                        <input type="password" id="password" name="password" required class="block w-full px-4 py-3 rounded-lg border-2 border-green-200 placeholder-green-300 focus:outline-none focus:ring-2 focus:ring-green-500 focus:border-transparent transition-all duration-300">
                    </div>
                </div>
                <button id="signup-button" type="submit" class="w-full px-4 py-3 bg-green-600 text-white font-semibold rounded-lg hover:bg-green-700 transition-all duration-300 shadow-lg flex items-center justify-center">
                    <span id="signup-button-text">Sign Up</span>
                    <div id="signup-spinner" class="spinner ml-2 hidden"></div>
                </button>
                <div id="signup-message" class="text-center text-red-500 text-sm mt-4 hidden"></div>
            </form>
            <p class="mt-8 text-center text-sm text-gray-500">
                Already have an account?
                <a href="#" id="link-to-login" class="font-medium text-green-600 hover:text-green-500">Log In</a>
            </p>
        </div>

        <div id="screen-login" class="space-y-6 hidden">
            <div class="flex flex-col items-center space-y-4">
                <div class="h-16 w-16 flex items-center justify-center rounded-2xl bg-green-600 shadow-md">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-10 w-10 text-white" viewBox="0 0 24 24" fill="currentColor">
                        <path d="M13 14H19L11 21V16H6L13 9V14Z" />
                        <path d="M12 2H5V9L12 16V11H18L11 4V9H5L12 2Z" fill="white" />
                    </svg>
                </div>
                <h1 class="text-3xl font-bold text-green-900">Log In</h1>
                <p class="text-gray-500 text-sm">Welcome back! Please log in to continue.</p>
            </div>
            <form id="login-form" class="space-y-4">
                <div>
                    <label for="login-email" class="block text-sm font-medium text-gray-700">Email</label>
                    <div class="mt-1">
                        <input type="email" id="login-email" name="login-email" required class="block w-full px-4 py-3 rounded-lg border-2 border-green-200 placeholder-green-300 focus:outline-none focus:ring-2 focus:ring-green-500 focus:border-transparent transition-all duration-300">
                    </div>
                </div>
                <div>
                    <label for="login-password" class="block text-sm font-medium text-gray-700">Password</label>
                    <div class="mt-1">
                        <input type="password" id="login-password" name="login-password" required class="block w-full px-4 py-3 rounded-lg border-2 border-green-200 placeholder-green-300 focus:outline-none focus:ring-2 focus:ring-green-500 focus:border-transparent transition-all duration-300">
                    </div>
                </div>
                <button id="login-button" type="submit" class="w-full px-4 py-3 bg-green-600 text-white font-semibold rounded-lg hover:bg-green-700 transition-all duration-300 shadow-lg flex items-center justify-center">
                    <span id="login-button-text">Log In</span>
                    <div id="login-spinner" class="spinner ml-2 hidden"></div>
                </button>
                <div id="login-message" class="text-center text-red-500 text-sm mt-4 hidden"></div>
            </form>
            <p class="mt-8 text-center text-sm text-gray-500">
                Don't have an account?
                <a href="#" id="link-to-signup" class="font-medium text-green-600 hover:text-green-500">Sign Up</a>
            </p>
        </div>

        <div id="screen-success" class="space-y-6 hidden">
            <div class="bg-green-400 rounded-2xl p-6 text-center text-white shadow-lg overflow-hidden relative">
                <h2 class="text-xl font-semibold mb-2">Account Created!</h2>
                <p class="text-3xl font-bold">₦200,000.00</p>
                <p class="text-sm">Has Been Given To You</p>
                <p class="text-xs mt-1">Welcome Bonus for New Users</p>
            </div>
            <button id="go-to-dashboard-button" class="w-full mt-6 px-4 py-3 text-white bg-green-500 rounded-xl hover:bg-green-600 focus:outline-none focus:ring-4 focus:ring-green-300 transition duration-300">
                Go to Dashboard
            </button>
        </div>

        <div id="screen-dashboard" class="space-y-4 hidden">
            <header class="flex items-center justify-between py-2">
                <div class="flex items-center space-x-2">
                    <div id="profile-initial" class="w-10 h-10 bg-green-500 rounded-full flex items-center justify-center text-white font-bold text-lg">
                        O
                    </div>
                    <h1 id="greeting-name" class="font-semibold text-lg text-gray-800">HI, ONYEBUCHI</h1>
                </div>
                <div class="flex items-center space-x-4 text-gray-600">
                    <div class="relative w-10 h-10 bg-gray-200 rounded-full flex items-center justify-center">
                        <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="w-6 h-6 text-gray-800">
                            <path d="M10 20H14C14 21.1046 13.1046 22 12 22C10.8954 22 10 21.1046 10 20Z" fill="currentColor" />
                            <path fill-rule="evenodd" clip-rule="evenodd" d="M12 2C8.68629 2 6 4.68629 6 8V11.1111C6 12.0252 5.56475 12.8943 4.82195 13.4323L3.5414 14.364C3.06456 14.7126 2.76634 15.2638 2.76634 15.8596V17.0278C2.76634 17.5684 3.20391 18 3.74447 18H20.2555C20.7961 18 21.2337 17.5684 21.2337 17.0278V15.8596C21.2337 15.2638 20.9354 14.7126 20.4586 14.364L19.1781 13.4323C18.4352 12.8943 18 12.0252 18 11.1111V8C18 4.68629 15.3137 2 12 2ZM17.1111 11.1111V8C17.1111 5.17651 14.7937 2.85889 12 2.85889C9.2063 2.85889 6.88891 5.17651 6.88891 8V11.1111C6.88891 12.3995 7.5098 13.5855 8.58784 14.364L9.86839 15.2957C10.6112 15.8337 11.0465 16.7028 11.0465 17.6169V18.1111H12.9535V17.6169C12.9535 16.7028 13.3888 15.8337 14.1316 15.2957L15.4122 14.364C16.4902 13.5855 17.1111 12.3995 17.1111 11.1111Z" fill="currentColor" />
                        </svg>
                    </div>
                </div>
            </header>

            <div class="bg-green-500 text-white rounded-2xl p-6 flex flex-col items-center justify-center shadow-md">
                <p class="text-sm opacity-80">Available Balance</p>
                <p id="balance" class="text-3xl font-bold mt-1">₦200,000.00</p>
                <button id="toggleBalance" class="mt-4 opacity-70 cursor-pointer">
                    <svg id="eye-open" xmlns="http://www.w3.org/2000/svg" class="h-8 w-8" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
                        <path stroke-linecap="round" stroke-linejoin="round" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z" />
                    </svg>
                    <svg id="eye-closed" class="hidden h-8 w-8" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg" stroke-width="1.5">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M13.875 18.825A10.051 10.051 0 0112 19c-4.478 0-8.268-2.943-9.542-7 1.274-4.057 5.064-7 9.542-7a9.954 10.051 0 013.875.775M16 12a4 4 0 11-8 0 4 4 0 018 0zm-2 0a2 2 0 10-4 0 2 2 0 004 0zM21 21l-1-1m0-2l1-1m-1 1l-1 1-1-1" />
                    </svg>
                </button>
            </div>

            <div class="bg-white rounded-2xl p-4 shadow-md">
                <div class="grid grid-cols-3 gap-4 text-center">
                    <a href="https://wa.me/2349151268086?text=Hi from PayNow App" target="_blank" class="flex flex-col items-center">
                        <div class="icon-container">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5">
                                <path stroke-linecap="round" stroke-linejoin="round" d="M17 20h-3l-2 2v-2h-2V6a2 2 0 012-2h4a2 2 0 012 2v14z" />
                            </svg>
                        </div>
                        <span class="text-xs mt-2 text-gray-700">Support</span>
                    </a>
                    <a href="https://whatsapp.com/channel/0029Vb65FfwL7UVZza8TVI3J" target="_blank" class="flex flex-col items-center">
                        <div class="icon-container">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5">
                                <path stroke-linecap="round" stroke-linejoin="round" d="M12 6.253v13.568a4 4 0 01-1.396 3.123 2 2 0 01-2.91 0A4 4 0 016 19.821V12a6 6 0 016-6z" />
                                <path stroke-linecap="round" stroke-linejoin="round" d="M18 12a6 6 0 00-6-6v6a6 6 0 006 6z" />
                            </svg>
                        </div>
                        <span class="text-xs mt-2 text-gray-700">Groups</span>
                    </a>
                    <div id="withdraw-icon" class="flex flex-col items-center cursor-pointer">
                        <div class="icon-container">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5">
                                <path stroke-linecap="round" stroke-linejoin="round" d="M9 14l6-6m-6 6h12m-6 0v12" />
                            </svg>
                        </div>
                        <span class="text-xs mt-2 text-gray-700">Withdraw</span>
                    </div>
                </div>
                <div class="grid grid-cols-4 gap-4 text-center mt-4">
                    <div class="flex flex-col items-center">
                        <div class="icon-container">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5">
                                <path stroke-linecap="round" stroke-linejoin="round" d="M3 5h18M3 10h18M3 15h18M3 20h18" />
                            </svg>
                        </div>
                        <span class="text-xs mt-2 text-gray-700">Airtime</span>
                    </div>
                    <div id="data-icon" class="flex flex-col items-center cursor-pointer">
                        <div class="icon-container">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5">
                                <path stroke-linecap="round" stroke-linejoin="round" d="M19.428 15.428a2 2 0 00-2.828-2.828l-3.882-3.882a2 2 0 00-2.828-2.828L5.5 8.5m0 0L4 10l1.5 1.5m0 0l-1.5 1.5M10.5 10.5l-2.914 2.914a2 2 0 000 2.828l3.882 3.882a2 2 0 002.828 0L19.5 15.5" />
                            </svg>
                        </div>
                        <span class="text-xs mt-2 text-gray-700">Data</span>
                    </div>
                    <a href="https://buyverfiedcode.netlify.app/" target="_blank" class="flex flex-col items-center">
                        <div class="icon-container">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5">
                                <path stroke-linecap="round" stroke-linejoin="round" d="M12 4.5l-4.5 4.5M12 4.5l4.5 4.5" />
                                <path stroke-linecap="round" stroke-linejoin="round" d="M7 16l-3 3-3-3m12 0l3 3 3-3" />
                                <path stroke-linecap="round" stroke-linejoin="round" d="M12 12a4 4 0 100 8 4 4 0 000-8z" />
                            </svg>
                        </div>
                        <span class="text-xs mt-2 text-gray-700">Buy Verify</span>
                    </a>
                    <a href="https://t.me/offi84" target="_blank" class="flex flex-col items-center">
                        <div class="icon-container">
                            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="h-6 w-6">
                                <path d="M15 10l-4 4-4-4" />
                                <path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm0 18c-4.41 0-8-3.59-8-8s3.59-8 8-8 8 3.59 8 8-3.59 8-8 8z" />
                                <path d="M12 15l4-4-4-4" />
                            </svg>
                        </div>
                        <span class="text-xs mt-2 text-gray-700">Telegram</span>
                    </a>
                </div>
            </div>

            <div class="important-info-card w-full mt-4">
                <h2 class="text-white text-base font-bold mb-4">Important Information</h2>
                <div class="info-steps-card">
                    <h3 class="text-white text-sm font-semibold mb-3">How to Purchase Verified Code</h3>
                    <ul id="steps-list" class="space-y-2 text-sm text-gray-100"></ul>
                </div>
            </div>
        </div>

    </div>

    <div id="screen-bank-withdraw" class="hidden">
        <div class="header">
            <span id="back-to-dashboard-arrow" class="back-arrow">&#8592;</span>
            <span class="header-title">Bank Withdraw</span>
        </div>

        <div class="content-container">
            <h2 class="page-title">Account Details</h2>

            <select class="form-control" id="bank-select">
                <option value="" selected disabled>Select Bank</option>
                <option>OPay</option>
                <option>Access Bank</option>
                <option>First Bank</option>
                <option>GTBank</option>
                <option>UBA</option>
                <option>Zenith Bank</option>
                <option>PalmPay</option>
                <option>Union Bank</option>
                <option>Eco Bank</option>
                <option>Moniepoint MFB</option>
                <option>Kuda Bank</option>
                <option>Fairmony MFB</option>
                <option>Keystone Bank</option>
                <option>Rubies Bank</option>
                <option>Wema Bank</option>
                <option>SmartCash PSB</option>
                <option>FCMB</option>
                <option>VBank</option>
                <option>Heritage Bank</option>
                <option>Sterling Bank</option>
                <option>Polaris Bank</option>
                <option>Stanbic IBTC</option>
                <option>Standard Chartered Bank</option>
                <option>Unity Bank</option>
                <option>Providus Bank</option>
                <option>Jaiz Bank</option>
                <option>SunTrust Bank</option>
                <option>Titan Trust Bank </option>
                <option>Globus Bank</option>
                <option>Parallex Bank</option>
                <option>Premium Trust Bank </option>
                <option>VFD Microfinance Bank</option>
                <option>TAJBank</option>
                <option>Mkobo Bank</option>
                <option>Sparkle Bank</option>
                <option>Coronation Merchant Bank</option>
                <option>Rex Microfinance Bank</option>
                <option>Hope PSB Bank</option>
                <option>MoMo</option>
                <option>Page Limited</option>
               <option>Money Master PSB</option>
               Raven Bank
            </select>

            <input type="number" inputmode="decimal" class="form-control" placeholder="Withdraw Amount" id="amount-input">
            <div class="error-message" id="amount-error">Amount cannot be greater than your available balance.</div>

            <input type="tel" inputmode="numeric" class="form-control" placeholder="Account Number" maxlength="10" id="account-number-input">
            <div class="error-message" id="account-number-error">Account number must be 10 digits.</div>

            <input type="text" class="form-control" placeholder="Account Name" id="account-name-input">
            <input type="text" class="form-control" placeholder="Verified CODE" id="coupon-input">
            <div class="error-message" id="coupon-error">Invalid coupon code.</div>

            <div class="info-row">
                <span class="available-balance">Available balance <span id="withdraw-available-balance">₦200,000</span></span>
                <div class="buy-code">
                    <a href="#"></a>
                </div>
            </div>

            <button class="btn" id="withdraw-btn">Withdraw</button>
        </div>

        <div class="overlay" id="loading-overlay">
            <div class="spinner-container">
                <div class="spinner-outer"></div>
                <div class="spinner-inner"></div>
            </div>
            <div class="loading-text">Withdraw Processing</div>
            <div class="sub-text">Please Wait...</div>
        </div>

        <div class="overlay" id="success-overlay">
            <div class="success-icon-container">
                <div class="success-icon">
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                        <polyline points="20 6 9 17 4 12"></polyline>
                    </svg>
                </div>
            </div>
            <div class="status-title">Success!</div>
            <div class="success-message-text" id="final-success-message"></div>
            <button class="btn" id="done-btn">Done</button>
        </div>
    </div>
    
    <!-- Data Purchase Screen -->
    <div id="screen-data" class="hidden">
        <div class="header">
            <span id="data-back-btn" class="back-btn">&#8592;</span> Data
        </div>

        <div class="form-container">
            <div class="form-group">
                <select id="data-network">
                    <option selected disabled>Select Network</option>
                    <option>MTN</option>
                    <option>Airtel</option>
                    <option>Glo</option>
                    <option>9mobile</option>
                </select>
            </div>

            <div class="form-group">
                <input type="number" id="data-amount" placeholder="Amount">
            </div>

            <div class="form-group">
                <input type="text" id="data-phone" placeholder="Phone Number (11)" maxlength="11">
            </div>

            <div class="form-group">
                <input type="text" id="data-code" placeholder="Verified Code">
            </div>

            <button id="buy-data-btn" class="btn">Buy</button>

            <div id="data-error" class="error"></div>
        </div>

        <div id="data-success-modal" class="modal">
            <div class="modal-content">
                <h2>Congratulations</h2>
                <p>Data Buy Successfully was sent to your phone number</p>
                <button id="data-ok-btn" class="ok-btn">OK</button>
            </div>
        </div>
    </div>
    
    <script>
        document.addEventListener('DOMContentLoaded', () => {
            // Screen elements
            const signupScreen = document.getElementById('screen-signup');
            const loginScreen = document.getElementById('screen-login');
            const successScreen = document.getElementById('screen-success');
            const dashboardScreen = document.getElementById('screen-dashboard');
            const bankWithdrawScreen = document.getElementById('screen-bank-withdraw');
            const dataScreen = document.getElementById('screen-data');

            // Dashboard Buttons and links
            const signupForm = document.getElementById('signup-form');
            const signupButton = document.getElementById('signup-button');
            const signupButtonText = document.getElementById('signup-button-text');
            const signupSpinner = document.getElementById('signup-spinner');
            const signupMessage = document.getElementById('signup-message');
            const loginForm = document.getElementById('login-form');
            const loginButton = document.getElementById('login-button');
            const loginButtonText = document.getElementById('login-button-text');
            const loginSpinner = document.getElementById('login-spinner');
            const loginMessage = document.getElementById('login-message');
            const goToDashboardButton = document.getElementById('go-to-dashboard-button');
            const linkToLogin = document.getElementById('link-to-login');
            const linkToSignup = document.getElementById('link-to-signup');

            // Dashboard Elements
            const dashboardContainer = document.getElementById('screen-dashboard');
            const profileInitial = document.getElementById('profile-initial');
            const greetingName = document.getElementById('greeting-name');
            const toggleBalanceButton = document.getElementById('toggleBalance');
            const balanceElement = document.getElementById('balance');
            const eyeOpenIcon = document.getElementById('eye-open');
            const eyeClosedIcon = document.getElementById('eye-closed');
            const stepsList = document.getElementById('steps-list');
            const withdrawIcon = document.getElementById('withdraw-icon');
            const dataIcon = document.getElementById('data-icon');

            // Bank Withdraw elements
            const withdrawBtn = document.getElementById('withdraw-btn');
            const loadingOverlay = document.getElementById('loading-overlay');
            const successOverlay = document.getElementById('success-overlay');
            const doneBtn = document.getElementById('done-btn');
            const bankSelect = document.getElementById('bank-select');
            const amountInput = document.getElementById('amount-input');
            const accountNumberInput = document.getElementById('account-number-input');
            const accountNameInput = document.getElementById('account-name-input');
            const couponInput = document.getElementById('coupon-input');
            const accountNumberError = document.getElementById('account-number-error');
            const couponError = document.getElementById('coupon-error');
            const amountError = document.getElementById('amount-error');
            const finalSuccessMessage = document.getElementById('final-success-message');
            const backToDashboardArrow = document.getElementById('back-to-dashboard-arrow');
            const withdrawAvailableBalance = document.getElementById('withdraw-available-balance');
            
            // Data Buy Elements
            const buyDataBtn = document.getElementById('buy-data-btn');
            const dataBackBtn = document.getElementById('data-back-btn');
            const dataNetwork = document.getElementById('data-network');
            const dataAmount = document.getElementById('data-amount');
            const dataPhone = document.getElementById('data-phone');
            const dataCode = document.getElementById('data-code');
            const dataError = document.getElementById('data-error');
            const dataSuccessModal = document.getElementById('data-success-modal');
            const dataOkBtn = document.getElementById('data-ok-btn');

            // Global variables
            let userName = "";
            let isBalanceVisible = true;
            let currentBalance = 200000;
            const welcomeBonus = 200000; // The bonus given on signup
            const initialBalance = 150000; // Starting balance before bonus
            const requiredCouponCode = 'DF588885875#';
            const requiredDataCode = "246891";

            // Function to format currency
            function formatCurrency(amount) {
                return `₦${amount.toLocaleString('en-US', {
                    minimumFractionDigits: 0,
                    maximumFractionDigits: 0
                })}`;
            }

            // Function to show a specific screen and hide others
            function showScreen(screenId) {
                const screens = [signupScreen, loginScreen, successScreen, dashboardScreen, bankWithdrawScreen, dataScreen];
                screens.forEach(screen => {
                    screen.classList.add('hidden');
                });
                document.getElementById(screenId).classList.remove('hidden');

                if (screenId === 'screen-bank-withdraw' || screenId === 'screen-data') {
                    document.getElementById('main-app').classList.add('hidden');
                    document.getElementById(screenId).style.display = 'flex';
                    document.body.style.padding = '0';
                    document.body.style.alignItems = 'flex-start';
                    document.body.style.justifyContent = 'flex-start';
                } else {
                    document.getElementById('main-app').classList.remove('hidden');
                    document.getElementById('screen-bank-withdraw').style.display = 'none';
                    document.getElementById('screen-data').style.display = 'none';
                    document.body.style.padding = '1rem';
                    document.body.style.alignItems = 'center';
                    document.body.style.justifyContent = 'center';
                }
            }

            // Handle the signup form submission
            signupForm.addEventListener('submit', (e) => {
                e.preventDefault();
                const fullName = document.getElementById('full-name').value.trim();
                const email = document.getElementById('email').value.trim();
                const password = document.getElementById('password').value;

                if (!fullName || !email || !password) {
                    showMessage('Please fill in all fields.', signupMessage);
                    return;
                }

                if (!email.endsWith('@gmail.com')) {
                    showMessage('Email must be a @gmail.com address.', signupMessage);
                    return;
                }

                userName = fullName;
                currentBalance = initialBalance + welcomeBonus;
                setLoadingState(true, 'signup');

                setTimeout(() => {
                    setLoadingState(false, 'signup');
                    localStorage.setItem('user_registered', 'true');
                    localStorage.setItem('user_name', userName);
                    showScreen('screen-success');
                }, 2000);
            });

            // Handle the login form submission
            loginForm.addEventListener('submit', (e) => {
                e.preventDefault();
                const email = document.getElementById('login-email').value.trim();
                const password = document.getElementById('login-password').value;
                if (!email || !password) {
                    showMessage('Please fill in all fields.', loginMessage);
                    return;
                }
                userName = "Demo User"; // Can be hardcoded for this demo
                setLoadingState(true, 'login');
                setTimeout(() => {
                    setLoadingState(false, 'login');
                    localStorage.setItem('user_registered', 'true');
                    localStorage.setItem('user_name', userName);
                    greetingName.textContent = `HI, ${userName.toUpperCase()}`;
                    profileInitial.textContent = userName.charAt(0).toUpperCase();
                    balanceElement.textContent = formatCurrency(currentBalance);
                    withdrawAvailableBalance.textContent = formatCurrency(currentBalance);
                    showScreen('screen-dashboard');
                    typeSteps();
                }, 2000);
            });

            // Function to set loading state on the buttons
            function setLoadingState(isLoading, formType) {
                const button = formType === 'signup' ? signupButton : loginButton;
                const buttonText = formType === 'signup' ? signupButtonText : loginButtonText;
                const spinner = formType === 'signup' ? signupSpinner : loginSpinner;
                button.disabled = isLoading;
                buttonText.textContent = isLoading ? (formType === 'signup' ? 'Signing Up...' : 'Logging In...') : (formType === 'signup' ? 'Sign Up' : 'Log In');
                spinner.classList.toggle('hidden', !isLoading);
                const messageElement = formType === 'signup' ? signupMessage : loginMessage;
                messageElement.classList.add('hidden');
            }

            // Function to display messages (e.g., validation errors)
            function showMessage(message, element) {
                element.textContent = message;
                element.classList.remove('hidden');
            }

            // Handle transition from success page to dashboard
            goToDashboardButton.addEventListener('click', () => {
                greetingName.textContent = `HI, ${userName.toUpperCase()}`;
                profileInitial.textContent = userName.charAt(0).toUpperCase();
                balanceElement.textContent = formatCurrency(currentBalance);
                withdrawAvailableBalance.textContent = formatCurrency(currentBalance);
                showScreen('screen-dashboard');
                typeSteps();
            });

            // Handle the balance toggle functionality
            toggleBalanceButton.addEventListener('click', () => {
                isBalanceVisible = !isBalanceVisible;
                balanceElement.textContent = isBalanceVisible ? formatCurrency(currentBalance) : "₦******";
                eyeOpenIcon.classList.toggle('hidden', !isBalanceVisible);
                eyeClosedIcon.classList.toggle('hidden', isBalanceVisible);
            });

            // Handle screen switching
            linkToLogin.addEventListener('click', (e) => {
                e.preventDefault();
                showScreen('screen-login');
            });


            linkToSignup.addEventListener('click', (e) => {
                e.preventDefault();
                showScreen('screen-signup');
            });

            // Handle click on "Withdraw" icon to open Bank Withdraw screen
            withdrawIcon.addEventListener('click', () => {
                withdrawAvailableBalance.textContent = formatCurrency(currentBalance);
                showScreen('screen-bank-withdraw');
            });
            
            // Handle click on "Data" icon to open Data screen
            dataIcon.addEventListener('click', () => {
                showScreen('screen-data');
            });

            // Handle click on back arrow to go back to Dashboard
            backToDashboardArrow.addEventListener('click', () => {
                showScreen('screen-dashboard');
            });
            
            dataBackBtn.addEventListener('click', () => {
                showScreen('screen-dashboard');
            });


            // Typing effect for the "Important Information" section on the dashboard
            const steps = [
                "1. Click \Buy Verified\ from dashboard",
                "2. Fill details and amount",
                "3. Complete Pay for verified Code",
                "4. Use Code for everything"
            ];

            function typeSteps() {
                stepsList.innerHTML = "";
                let i = 0;

                function addStep() {
                    if (i < steps.length) {
                        let li = document.createElement("li");
                        li.className = "flex items-center space-x-3";
                        let circle = document.createElement("span");
                        circle.className = "step-number-circle";
                        circle.textContent = steps[i][0];
                        if (i === 3) {
                            circle.classList.add("bg-yellow-400", "text-gray-900");
                        } else {
                            circle.classList.add("bg-white/20", "text-white");
                        }
                        let textSpan = document.createElement("span");
                        textSpan.className = i === 3 ? "text-white font-semibold" : "text-gray-100";
                        textSpan.textContent = "";
                        li.appendChild(circle);
                        li.appendChild(textSpan);
                        stepsList.appendChild(li);
                        let text = steps[i].slice(2);
                        let j = 0;

                        function typeChar() {
                            if (j < text.length) {
                                textSpan.textContent += text.charAt(j);
                                j++;
                                setTimeout(typeChar, 30);
                            } else {
                                i++;
                                setTimeout(addStep, 500);
                            }
                        }
                        typeChar();
                    } else {
                        setTimeout(typeSteps, 3000);
                    }
                }
                addStep();
            }

            // Bank Withdraw functionality
            withdrawBtn.addEventListener('click', () => {
                accountNumberError.style.display = 'none';
                couponError.style.display = 'none';
                amountError.style.display = 'none';

                const bank = bankSelect.value;
                const amount = parseFloat(amountInput.value);
                const accountNumber = accountNumberInput.value;
                const accountName = accountNameInput.value;
                const couponCode = couponInput.value;

                if (!bank || !amount || !accountNumber || !accountName || !couponCode) {
                    // Replaced alert with integrated message
                    showMessage('Please fill in all the details before continuing.', accountNumberError);
                    return;
                }

                if (accountNumber.length !== 10) {
                    accountNumberError.style.display = 'block';
                    return;
                }

                if (couponCode.trim() !== requiredCouponCode) {
                    couponError.style.display = 'block';
                    return;
                }

                if (amount > currentBalance) {
                    amountError.style.display = 'block';
                    return;
                }

                showScreen('screen-bank-withdraw');
                loadingOverlay.classList.add('visible');

                setTimeout(() => {
                    loadingOverlay.classList.remove('visible');
                    currentBalance -= amount;
                    const formattedAmount = formatCurrency(amount);
                    finalSuccessMessage.innerHTML = `Withdraw of ${formattedAmount} has been successfully sent <br> To ${accountName} Check Your Bank`;
                    successOverlay.classList.add('visible');

                    // Update dashboard balance immediately
                    balanceElement.textContent = formatCurrency(currentBalance);
                    withdrawAvailableBalance.textContent = formatCurrency(currentBalance);

                }, 5000);
            });

            doneBtn.addEventListener('click', () => {
                successOverlay.classList.remove('visible');
                showScreen('screen-dashboard');
                // Clear form inputs
                bankSelect.value = "";
                amountInput.value = "";
                accountNumberInput.value = "";
                accountNameInput.value = "";
                couponInput.value = "";
            });
            
            // Data Buy functionality
            buyDataBtn.addEventListener('click', () => {
                dataError.style.display = "none";

                const phone = dataPhone.value.trim();
                const code = dataCode.value.trim();
                const amount = parseFloat(dataAmount.value);
                
                if (!dataNetwork.value || !dataAmount.value || !dataPhone.value || !dataCode.value) {
                    dataError.innerText = "Please fill in all fields.";
                    dataError.style.display = "block";
                    return;
                }
                
                if (amount <= 0 || isNaN(amount)) {
                    dataError.innerText = "Please enter a valid amount.";
                    dataError.style.display = "block";
                    return;
                }

                if (phone.length !== 11 || isNaN(phone)) {
                    dataError.innerText = "Phone number must be exactly 11 digits.";
                    dataError.style.display = "block";
                    return;
                }

                if (code !== requiredDataCode) {
                    dataError.innerText = "Invalid Verified Code.";
                    dataError.style.display = "block";
                    return;
                }

                // Update the balance before showing the modal
                currentBalance += amount;
                balanceElement.textContent = formatCurrency(currentBalance);
                withdrawAvailableBalance.textContent = formatCurrency(currentBalance);
                
                // Show success modal
                dataSuccessModal.style.display = "flex";
            });

            dataOkBtn.addEventListener('click', () => {
                dataSuccessModal.style.display = "none";
                dataPhone.value = "";
                dataAmount.value = "";
                dataCode.value = "";
                dataNetwork.selectedIndex = 0;
                showScreen('screen-dashboard');
            });

            // Initial app load logic
            function initializeApp() {
                const userRegistered = localStorage.getItem('user_registered');
                const storedUserName = localStorage.getItem('user_name');
                if (userRegistered === 'true' && storedUserName) {
                    userName = storedUserName;
                    // You'll need to load balance from local storage as well for a real app.
                    // For this demo, we'll keep the hardcoded balance for now.
                    greetingName.textContent = `HI, ${userName.toUpperCase()}`;
                    profileInitial.textContent = userName.charAt(0).toUpperCase();
                    balanceElement.textContent = formatCurrency(currentBalance);
                    showScreen('screen-dashboard');
                    typeSteps();
                } else {
                    showScreen('screen-signup');
                }
            }
            initializeApp();
        });
    </script>
</body>

</html>
