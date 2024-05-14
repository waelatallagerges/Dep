# Integration with Cisco

## DEP Platform Integration with Cisco Finesse Widget

## Overview
This documentation outlines the integration process between the DEP (Digital Engagement Platform ) platform and Cisco Finesse Widget. The integration involves sending notifications from DEP to a middleware (Node.js application), which then communicates with the Cisco Finesse Gadget via WebSockets. Finesse responds to the notifications by making API calls back to DEP.

## Integration Steps

### 1. Setup Node.js Middleware
1. Install Node.js if not already installed.
2. Create a new Node.js project or use an existing one.
3. Install necessary dependencies using npm:
4. Create an Express server to handle incoming requests.
5. Implement WebSocket functionality using Socket.IO to communicate with the Finesse Gadget.

### 2. Configure DEP Webhook
1. Access the DEP platform dashboard.
2. Navigate to the webhook configuration section.
3. Add a new webhook endpoint pointing to the Node.js middleware server's URL.
4. Configure the webhook to send relevant notifications to the middleware.

### 3. Implement Notification Handling in Middleware
1. Define WebSocket handlers in the Node.js application to receive notifications from DEP.
2. Parse and process incoming notifications as per application requirements.
3. Establish a WebSocket connection with the Finesse Gadget using Socket.IO.
4. Forward processed notifications to the Finesse Gadget via WebSocket communication.

### 4. Cisco Finesse Gadget Setup
1. Access the Cisco Finesse Gadget development environment.
2. Create or update the gadget to handle incoming notifications from the middleware.
3. Implement WebSocket connection handling to receive notifications from the middleware.
4. Process incoming notifications and perform necessary actions within the Finesse Gadget UI.

### 5. Finesse API Integration
1. Define API endpoints in the Node.js middleware to handle responses from Finesse.
2. Implement logic to process API calls from Finesse and update DEP accordingly.
3. Secure API endpoints with appropriate authentication mechanisms if required.

##### Upon successful integration and configuration:

* DEP will send notifications to the Node.js middleware via webhook.
* The middleware will handle and forward notifications to the Cisco Finesse Gadget through WebSocket communication.
* The Finesse Gadget will process notifications and interact with Finesse API as needed.
* Responses from Finesse API will be handled by the middleware and updated back in DEP as per integration logic.

Example Code (Node.js Middleware) 
```bash
// Express server setup
const express = require('express');
const http = require('http');
const socketIo = require('socket.io');
const axios = require('axios');

const app = express();
const server = http.createServer(app);
const io = socketIo(server);

// Handle incoming DEP notifications via webhook
app.post('/webhook', (req, res) => {
const notification = req.body; // Assuming JSON payload
// Process notification and forward to Finesse Gadget
io.emit('dep_notification', notification);
res.sendStatus(200);
});

// WebSocket connection with Finesse Gadget
io.on('connection', (socket) => {
console.log('Client connected');
// Handle incoming messages from Finesse Gadget
socket.on('finesse_response', (response) => {
// Process Finesse response and update DEP if needed
axios.post('https://dep-api-endpoint.com/update', response)
.then(() => console.log('DEP updated'))
.catch((error) => console.error('Error updating DEP:', error));
});
});

// Start the server
const PORT = process.env.PORT || 3000;
server.listen(PORT, () => {
console.log(`Server running on port ${PORT}`);
});
---
```
this script code you will modified this websocket link with your new one :
```bash
<script type="text/javascript">
                var ch_connected = false;
                function connectWS(){
                    const ws = new WebSocket('wss://istwebsocket.a5c6cpcxhufhhdf9.westeurope.azurecontainer.io:4000');
                    ws.onopen = () => {
                        console.log("DEP_WS > connected");
                    };
           
                    ws.onmessage = (event) => {
                            console.log("DEP_WS > Event_message > " + event.data);
                            //const message = document.createElement('div');
                            if(ch_connected){
                                const parsedMessage = JSON.parse(event.data);
                                if (parsedMessage.event === 'keepalive' && parsedMessage.message && parsedMessage.message.message === 'keepalive') {
                                    console.log("DEP_WS > Keep-alive message received");    
                                } else {                                                
                                    console.log("DEP_WS > message recieved");
                                    digitalChannelHandler.handleShowPop(parsedMessage);                                
                                }                              
                           }        
                     };
           
                    ws.onerror = (error) => {
                        console.error('WebSocket error:', error);
                    };
           
                    ws.onclose = () => {
                        console.log("DEP_WS > disconnected");
                        setTimeout(function() { connectWS();}, 200);
                        //statusElement.textContent = 'Disconnected';
                        //statusElement.style.color = 'grey';
                    };
                }
                connectWS();
                function checkConnected() {
                    if (typeof gadgets.Hub != 'undefined' && gadgets.Hub.isConnected() && finesse != 'undefined' && digitalChannelHandler !='undefined') {
                        digitalChannelHandler.initialize();
                        ch_connected = true;
                    }
                    else {
                         setTimeout(checkConnected, 100);
                    }
                 };
 
                $(document).ready(function() {
                    checkConnected();
                });
            </script>
```
for more information [Cisco Finesse](https://developer.cisco.com/learning/labs/finesse-add-a-gadget/introduction/)