# 1. The Client-Server Model
* **Client**: The "front-facing" part of the application (your browser/UI) that users interact with.

* **Server**: A powerful computer that sits remotely, waiting for requests from the client to process data or perform logic.

* **Communication**: They communicate via HTTP requests. The client sends a "Request" (e.g., GET or POST), and the server sends back a "Response" (usually JSON data or HTML). When "Search" is clicked: The client captures the input, sends an API request to the server. The server fetches the latest price from a database or external provider and sends it back to the UI to be displayed.

# 2. Full-Stack Layers
* **Frontend**: The UI (HTML/CSS/JS) the user sees.

* **Backend**: The logic (Python, Node.js, etc.) that handles security and data processing.

* **Database**: Where data (user profiles, historical prices) is permanently stored.

* **APIs**: The "waiter" that takes your order (request) from the table (Frontend) to the kitchen (Backend) and brings back your food (Data).
