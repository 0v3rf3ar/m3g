# m3g

m3g is a powerful command-line utility by 0verf3ar designed for efficiently fetching multiple URLs using the requests library. With support for various HTTP methods, customizable headers, and options for concurrency, m3g simplifies the process of making bulk web requests. The dynamic user-agent rotation, configurable concurrency and delay time makes it so human-like and hard for WAF to detect. Ideal for developers, researchers and bounty hunters, m3g allows users to log responses, manage timeouts, and follow redirects, all while ensuring a smooth and user-friendly experience.

# Installation

To install m3g, you could simply use one of these two methods.
### Using curl:
```bash
cd
curl -o .m3g https://raw.githubusercontent.com/0v3rf3ar/m3g/refs/heads/main/m3g
echo "alias m3g='python3 ~/.m3g'" >> ~/.bashrc # or .zshrc
source ~/.bashrc # or .zshrc
```
### Using wget:
```bash
cd
wget -O .m3g https://raw.githubusercontent.com/0v3rf3ar/m3g/refs/heads/main/m3g
echo "alias m3g='python3 ~/.m3g'" >> ~/.bashrc # or .zshrc
source ~/.bashrc # or .zshrc
```
# Usage
```
usage: m3g [-h] [-t TARGET] [-f FILE] [-X REQUEST] [-T TIMEOUT] [-c CONCURRENCY] [-L] [-H HEADER] [-d DELAY] [-l LOG] [--silent]
            [--verbose]

Description: m3g is a powerful command-line utility by 0verf3ar designed for efficiently fetching multiple URLs using the requests
library. With support for various HTTP methods, customizable headers, and options for concurrency, m3g simplifies the process of
making bulk web requests. The dynamic user-agent rotation, configurable concurrency and delay time makes it so human-like and hard
for WAF to detect. Ideal for developers, researchers and bounty hunters, m3g allows users to log responses, manage timeouts, and
follow redirects, all while ensuring a smooth and user-friendly experience.

options:
  -h, --help            show this help message and exit
  -t TARGET, --target TARGET
                        Specify a domain with URL scheme e.g.(http://domain.com)
  -f FILE, --file FILE  Specify the file path containing URLs
  -X REQUEST, --request REQUEST
                        Specify the HTTP request method (e.g., GET, POST, PUT, DELETE, OPTIONS, TRACE, HEAD)
  -T TIMEOUT, --timeout TIMEOUT
                        Set the timeout for request (default: 10 seconds)
  -c CONCURRENCY, --concurrency CONCURRENCY
                        Set the concurrency level (default: 10)
  -L, --follow          Follow redirects (3xx)
  -H HEADER, --header HEADER
                        Specify a header in request
  -d DELAY, --delay DELAY
                        Set the delay time between request batches (default: no delay)
  -l LOG, --log LOG     Specify the log file path (default: request_log.txt)
  --silent              Suppress all terminal output (except errors)
  --verbose             Enable verbose mode with extra details in the terminal and output files
```
### Most basic example
This example specifies the target domain and a file containing URLs, using default options.
```bash
m3g -t http://example.com -f urls.txt
```
Explanation: This command will read URLs from urls.txt and send GET requests to each URL with default settings.

### Fastest Example
This example increases concurrency to the maximum (50) and sets a very short timeout (1 second).
```bash
m3g -t http://example.com -f urls.txt -c 50 -T 1
```
Explanation: This command will quickly send up to 50 concurrent GET requests with a timeout of 1 second for each request, maximizing speed.

### Careful to Not Get Recognized by WAF
This example uses a delay between batches, random user agents, and a moderate concurrency level.
```bash
m3g -t http://example.com -f urls.txt -c 10 -d 5 --silent
```
Explanation: This command sends GET requests to URLs in urls.txt with 10 concurrent requests, a 5-second delay between batches, and suppresses terminal output to make it less detectable by WAFs.

### Bounty Hunter Use Case
This example uses a custom header (like a CSRF token), verbose output for detailed logging, and follows redirects.
```bash
m3g -t http://example.com -f urls.txt -H "X-CSRF-Token: your_csrf_token" -L -l log.txt -L --verbose -X POST
```
Explanation: This command sends POST requests to URLs with a custom CSRF token header, logs the output to log.txt, enables verbose output for debugging, and allows for easy tracking of responses.
