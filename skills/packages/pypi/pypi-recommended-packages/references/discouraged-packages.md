# Discouraged Packages

**requests**: [github](https://github.com/psf/requests) #http #timeout\
Requests has no default timeout, so requests can hang when callers do not set one explicitly. The proposal to require or provide a default timeout was closed without changing this behavior: [psf/requests#3070](https://github.com/psf/requests/issues/3070).
