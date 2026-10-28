# Discouraged Packages

**httpx**: [github](https://github.com/encode/httpx) #http #maintenance\
Prefer httpx2 because HTTPX has seen limited maintenance: its [latest stable PyPI release](https://pypi.org/project/httpx/) was published in December 2024, while [httpx2](https://github.com/pydantic/httpx2) continues development under Pydantic. Check the [migration guide](https://pydantic.dev/docs/httpx2/get-started/migration/) for Python version and integration compatibility.

**requests**: [github](https://github.com/psf/requests) #http #timeout\
Requests has no default timeout, so requests can hang when callers do not set one explicitly. The proposal to require or provide a default timeout was closed without changing this behavior: [psf/requests#3070](https://github.com/psf/requests/issues/3070).
