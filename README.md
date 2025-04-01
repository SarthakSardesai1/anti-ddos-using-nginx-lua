# Anti-DDoS Challenge Script

## Overview

This project is a Lua script designed to help protect websites from distributed denial-of-service (DDoS) attacks. In simple terms, it makes sure that the people visiting your site are real users and not harmful bots or hackers. It does this by checking each visitor’s details and requiring a quick "puzzle" to be solved in the browser before granting access.

## Features

- **Customizable Security Settings**  
  You can set a secret key and adjust how long a visitor stays authenticated. This means you have control over how strict or lenient the protection is.

- **Automatic Client Identification**  
  The script is smart enough to automatically grab the visitor’s IP address from different sources (like proxies or Cloudflare) so that it knows who is trying to access your site.

- **Dynamic JavaScript Puzzle**  
  To check that visitors are using real web browsers, the script sends a small puzzle to be solved by JavaScript. This puzzle changes every day, making it hard for bots to guess.

- **Header and Cookie Management**  
  It modifies response headers and cookies to both hide server details and enforce security. For example, it can remove information that might reveal what software the server is running.

- **Query String and IP Address Filtering**  
  The script cleans up any unnecessary or harmful parts of URLs (query strings) and can block visitors based on their IP address or if they appear to be from a blacklisted range.

- **Support for Tor and Various User Agents**  
  It can either allow or block access from Tor users, and it checks the user’s browser details (user-agent) to further protect against known bad bots.

## How It Works

1. **Visitor Identification:**  
   When someone visits your site, the script automatically finds out their IP address using several different methods. This helps in uniquely identifying each visitor.

2. **Security Checks:**  
   The script runs a set of checks in the background:
   - It looks at the visitor’s browser information to make sure it isn’t a hidden bot.
   - It sends a simple JavaScript puzzle to the visitor’s browser that must be solved correctly before allowing access.
   - It checks for any suspicious URL parts or query strings that might be used to bypass caching or launch an attack.

3. **Request Filtering:**  
   If any unusual or dangerous behavior is detected, the script can block the visitor by dropping specific headers or even the request itself. This keeps the server safe from overloads and potential attacks.

4. **Custom Headers and Cookies:**  
   The script sets custom headers and cookies to maintain a secure session for the visitor. These settings can be customized so that even if someone tries to mimic a legitimate request, they won’t pass the checks.

## Configuration and Function Descriptions

This project is built around a series of configuration options and functions. Here’s a brief look at some of the key functions and what they do:

- **Client IP Detection:**  
  Automatically selects the best available IP address from headers like `http_cf_connecting_ip`, `http_x_forwarded_for`, or `remote_addr`. This ensures reliable identification even when traffic goes through proxies.

- **Header Modification:**  
  Functions in this section go through a list of custom header rules to either set or remove certain headers. This helps hide sensitive information (like server software details) and improves cache performance.

- **Query String Cleanup:**  
  There are functions designed to remove unwanted parts of the URL. This helps to keep the cache effective and stops attackers from using extra URL parameters to bypass security.

- **JavaScript Puzzle Generation:**  
  A small part of the script generates a daily-changing puzzle using date values. Both the JavaScript and Lua parts of the script calculate the answer to this puzzle, ensuring that only a correct, synchronized response will pass the check.

- **IP Range Check:**  
  Functions check whether the visitor’s IP falls within a defined safe or dangerous range. This is useful for blocking known problematic networks.

- **User-Agent Blacklist and Whitelist:**  
  These parts of the script compare the visitor’s browser details against a list of known bad or good agents. It helps in quickly blocking suspicious visitors while allowing trusted ones.

## For Non-Developers

Imagine your website is like a busy café. You want to make sure that everyone coming in is a real person and not a robot trying to disrupt your service. This script works like a friendly bouncer who:
- Checks IDs (IP addresses) using various methods.
- Gives a quick riddle (the JavaScript puzzle) that only genuine café-goers can solve.
- Keeps an eye out for any suspicious behavior (weeding out bad guests) by checking the way they enter (headers, query strings, etc.).

With these layers of checks, your site remains open and welcoming to real users while keeping troublemakers out.

## Getting Started

1. **Download or Clone the Repository:**  
   Begin by downloading or cloning the repository to your local machine.

2. **Edit the Configuration:**  
   Open the Lua script and change the default secret key and any other settings as needed for your website’s security requirements.

3. **Deploy the Script:**  
   Follow the deployment instructions specific to your web server or hosting platform. This script is meant to be integrated with servers that support Lua, like those using Nginx with the Lua module.

4. **Test Your Setup:**  
   Visit your website from different browsers and networks to ensure the script correctly authenticates visitors and blocks unwanted traffic.

## Final Notes

This project is an easy-to-customize tool to enhance your website’s security. Whether you run a small blog or a large e-commerce site, the script is designed to be adjusted to your needs while remaining simple enough for non-technical users to understand.

---
