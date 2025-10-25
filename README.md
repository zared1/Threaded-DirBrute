# Threaded-DirBrute

A small, multithreaded directory brute‑forcer that reads paths from a wordlist and checks `URL + path` concurrently. Fast, simple, and built for quick reconnaissance or lab testing.

## Features

* Multithreaded HTTP GET requests using Python `requests`
* Reads paths from a plain text wordlist (one path per line)
* Prints discovered paths that return `200 OK`
* Simple CLI: specify target URL, wordlist, and thread count

## How to Run

1. Clone or download the repo.
2. Install dependencies (only `requests` is required):

```bash
pip install requests
```

3. Run the script:

```bash
python multithreaded.py <url> <wordlist> [--threads N]
# Examples:
python multithreaded.py https://example.com ./wordlists/common.txt
python multithreaded.py https://example.com ./wordlists/common.txt --threads 20
```

**Wordlist format:** one path per line, for example:

```
admin
robots.txt
uploads/
images
secret.php
```

The script appends each line directly to the provided URL; include trailing slashes in wordlist entries if needed.

## Notes

* This tool is for **educational / authorized testing only**. Do not run it against systems you do not own or have permission to test. Unauthorized scanning may be illegal.
* Default thread count is 10 — increase for speed, but be mindful of target load and rate limits.
* Only prints paths returning HTTP 200. You can extend it to log other status codes (301/403/etc.) or save results to a file.
* Possible improvements:

  * Add per-request timeouts and retry logic (`requests.get(..., timeout=...)`)
  * Add rate limiting or delays to reduce server load
  * Support resume, output file, and filtering by status code
  * Use a thread-safe queue to split work across threads more efficiently
