# Discouraged Packages

**httpx**: [github](https://github.com/encode/httpx) #http #maintenance\
Prefer httpx2 because HTTPX's [latest stable PyPI release](https://pypi.org/project/httpx/) dates to December 2024 as of 2026-10-29, while [httpx2](https://github.com/pydantic/httpx2) continues development under Pydantic. HTTPX's [release history](https://pypi.org/project/httpx/#history) also includes 1.0.dev pre-releases from August 2026, so this preference concerns stable-release cadence rather than an absence of development. Check the [migration guide](https://pydantic.dev/docs/httpx2/get-started/migration/) for Python version and integration compatibility.

**requests**: [github](https://github.com/psf/requests) #http #timeout\
Requests has no default timeout, so requests can hang when callers do not set one explicitly. The proposal to require or provide a default timeout was closed without changing this behavior: [psf/requests#3070](https://github.com/psf/requests/issues/3070).
