# Authentication

When you log in on the Roblox website, you create a new session with a special identifier linked to it, and that token is stored on your computer as a cookie.
Every single time your computer asks Roblox to do anything - for example, "give me the name of this user" - your computer also gives this token to Roblox, and it can look and see if that token is valid.  

Let's say you're asking Roblox to give you a list of your friends. It'll look at that token and know who you are, and can use that to give you your friends list.

```mermaid
sequenceDiagram
    participant Client
    participant Server
    Client->>Server: Hello, can I log in? Here's my username and password.
    Note left of Server: Server makes a token and stores it, and then gives it to the client.
    Server->>Client: Okay! Here's your token.
    Note right of Client: Token is stored in the cookies.
    Client->>Server: Hello! Can you give me a list of my friends? Here is my cookie.
    Note left of Server: Server sees token in cookies and uses it to get their friend list.
    Server->>Client: Okay! Here is your friends list.
```

When you log out, that token is invalidated. Even if the client holds on to the token, it won't be valid after logging out.

```mermaid
sequenceDiagram
    participant Client
    participant Server
    Client->>Server: Hello, can I log out?
    Note left of Server: Server deletes the token from its storage.
    Server->>Client: Okay! Please delete your token.
    Note right of Client: Token is deleted from cookies.
    Client->>Server: Hello! Can you give me a list of my friends? Here is my cookie.
    Note left of Server: Client has no token, so server responds with an error.
    Server->>Client: Sorry, you aren't logged in.
```

This token is called the `.ROBLOSECURITY` token and you will need one to do anything that you need to be logged in to do on Roblox, including:  

- getting information about yourself (name, description, id, etc)  
- changing avatar  
- getting friends list  
- playing games  

With ro.py, we're going to skip actually asking the server to log us in.
We're just going to log in on the Roblox website and then copy the cookie from our web browser and use it in our code.  

!!! danger
    Make sure you do not share this token! Anyone with the token essentially has full access to your account.

!!! warning
    As stated earlier, pressing the "Log out" button invalidates your token, so you should not press this button after grabbing your token.

To grab your .ROBLOSECURITY cookie, follow the instructions below for your web browser.

=== "Chrome/Chromium-based"
    You can access the cookie by going to https://www.roblox.com/, pressing the padlock icon next to the URL in your
    browser, clicking the arrow next to `roblox.com`, opening up the "Cookies" folder, clicking ".ROBLOSECURITY",
    clicking on the "Content" text once, pressing ++control+a++, and then pressing ++control+c++
    (make sure **not** to double-click this field as you won't select the entire value!)  
    
    ![](/assets/screenshots/ChromeCookie.png){: style="width: 400px"}
    
    Alternatively, you can access the cookie by going to https://www.roblox.com/, pressing ++control+shift+i++ to access
    the Developer Tools, navigating to the "Application" tab, opening up the arrow next to "Cookies" on the sidebar on
    the left, clicking the `https://www.roblox.com` item underneath the Cookies button, and then copying the
    .ROBLOSECURITY token by double-clicking on the value and then hitting ++control+c++.
    
    ![](/assets/screenshots/ChromeDevTools.png){: style="height: 436px"}
=== "Firefox"
    You can access the cookie by going to https://www.roblox.com/ and pressing ++shift+f9++,
    pressing the "Storage" tab button on the top, opening up the "Cookies" section in the sidebar on the left, 
    clicking the `https://www.roblox.com` item underneath it,
    and then copying the .ROBLOSECURITY token by double-clicking on the value and then hitting ++control+c++.
    ![](/assets/screenshots/FirefoxCookie.jpeg)