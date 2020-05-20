When you open a new window using the `target="_blank"` attribute, the new window has a window.opener property that points to the parent 
window and can run on the same process. Because it has access to the parent window's window.opener property, it can redirect your 
page to a malicious URL. 

Solution: Add `rel="noopener noreferrer"` to the `<a>` element. That creates a new process so that the new window doesn't have 
access to the parent window.

https://bolajiayodeji.com/the-security-vulnerabilities-of-the-target_blank-attribute-cka3hgvyw01axdjs13r1xgc7m
