



# Gobuster Lesson 06 — Output Saving & Wildcard Response Analysis

## Objective

Learn how to save Gobuster directory-enumeration results to a file and identify false-positive responses caused by a wildcard/custom server response.

## Target

```text
http://192.168.0.1
```

This was performed against my own local lab/router environment.

## Wordlist

```text
/usr/share/wordlists/dirb/common.txt
```

Wordlist size:

```text
36K
```

## Initial Gobuster Command

```bash
gobuster dir -u http://192.168.0.1 \
-w /usr/share/wordlists/dirb/common.txt \
-o gobuster-lesson-06.txt
```

Gobuster detected that a random, non-existing URL returned:

```text
HTTP Status: 200
Content Length: 151
```

Because the server returned the same response for non-existing paths, Gobuster stopped to prevent false-positive results.

## Random URL Verification

Command:

```bash
curl -s -o /tmp/random-response.txt \
-w 'HTTP=%{http_code} SIZE=%{size_download}\n' \
http://192.168.0.1/this-is-a-random-test-12345
```

Result:

```text
HTTP=200 SIZE=151
```

File size verification:

```bash
wc -c /tmp/random-response.txt
```

Result:

```text
151 /tmp/random-response.txt
```

The response body contained a JavaScript redirect to:

```text
/login.htm
```

This confirmed that the `200/151` response was a common login-related response rather than proof that the requested path existed.

## Corrected Gobuster Scan

To exclude the known wildcard response length:

```bash
gobuster dir -u http://192.168.0.1 \
-w /usr/share/wordlists/dirb/common.txt \
-o gobuster-lesson-06.txt \
--exclude-length 151
```

Final scan:

```text
Progress: 4613 / 4613 (100.00%)
Finished
```

## Output Verification

```bash
ls -lh gobuster-lesson-06.txt
```

Result:

```text
-rw-rw-r-- 1 pradyut pradyut 0 Sep 16 21:36 gobuster-lesson-06.txt
```

And:

```bash
wc -c gobuster-lesson-06.txt
```

Result:

```text
0 gobuster-lesson-06.txt
```

## Interpretation

The empty output file does not mean that Gobuster failed.

The scan completed successfully, but after excluding the known `151`-byte wildcard/login response, no unique results from the tested wordlist were identified.

## Key Lessons

* `-u` specifies the target URL.
* `-w` specifies the wordlist.
* `-o` saves Gobuster output to a file.
* HTTP `200` does not automatically mean that a resource exists.
* Response length can help identify false positives.
* Response body analysis can reveal a common login/error response.
* `--exclude-length` can remove a known wildcard response from the results.
* An empty output file can be a legitimate enumeration result.
* Scan completion and findings are two different things.

## Evidence

```text
Target: http://192.168.0.1
Wordlist: common.txt
Entries tested: 4613
Wildcard response: 200 / 151 bytes
Excluded length: 151
Scan status: Completed
Unique findings: None identified
Output file: gobuster-lesson-06.txt
Output size: 0 bytes
```

## Ethical Scope

This exercise was performed against a device in my own local lab environment for cybersecurity learning and enumeration practice.
