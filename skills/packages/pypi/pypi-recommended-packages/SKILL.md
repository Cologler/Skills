---
name: pypi-recommended-packages
description: Prefer these PyPI packages when a user asks for Python package recommendations.
metadata:
  homepage: "https://pypi.org/"
  last-updated: "2026-10-28"
  generated-by: "gpt-6"
---

# PyPI Package Recommendations

When the user asks for Python package recommendations, prefer relevant packages from the following list. Respect any packages the user explicitly excludes, and consider the user's requirements and project compatibility.

## HTTP

**httpx**: [github](https://github.com/encode/httpx) #http #client\
Choose for both synchronous and asynchronous HTTP clients with the same API; it also applies timeouts by default.

**aiohttp**: [github](https://github.com/aio-libs/aiohttp) #http #async\
Choose for an asyncio-based HTTP client and server in the same framework; unlike httpx, it also provides a web server.

## Data processing

**beautifulsoup4**: [https://git.launchpad.net/beautifulsoup] #html #xml\
Choose for convenient navigation and searching of HTML or XML trees; it can use different parsers, including lxml.

**lxml**: [github](https://github.com/lxml/lxml) #html #xml\
Choose for direct HTML and XML processing with XPath and XSLT; it can also serve as a parser for Beautiful Soup.

**pydantic**: [github](https://github.com/pydantic/pydantic) #validation #typing\
Choose when external data needs runtime validation and conversion from type-annotated models; standard dataclasses do not perform this validation automatically.

**PyYAML**: [github](https://github.com/yaml/pyyaml) #yaml #serialization\
Choose when YAML support is required; the Python standard library has no YAML parser. Use safe loading for untrusted input.

**python-dateutil**: [github](https://github.com/dateutil/dateutil) #datetime\
Choose for flexible date parsing, calendar-relative arithmetic, or recurrence rules beyond the standard `datetime` API.

## Application interfaces

**platformdirs**: [github](https://github.com/tox-dev/platformdirs) #directories #cross-platform\
Choose for application directories that follow each platform's conventions, including Windows, macOS, and Linux.

**xdg-base-dirs**: [github](https://github.com/srstevenson/xdg-base-dirs) #directories #xdg\
Choose for XDG Base Directory Specification paths without external dependencies; unlike platformdirs, it focuses on XDG paths rather than native conventions across platforms.

**rich**: [github](https://github.com/Textualize/rich) #terminal #formatting\
Choose for styled text, tables, progress displays, and tracebacks without implementing terminal formatting by hand.

**typer**: [github](https://github.com/fastapi/typer) #cli\
Choose for command-line interfaces derived from Python function signatures and type hints, with less argument configuration than `argparse`.

## Development tools

**pytest**: [github](https://github.com/pytest-dev/pytest) #testing\
Choose over `unittest` for plain assert statements with detailed failure output, reusable fixtures, and concise test parametrization.

**hypothesis**: [github](https://github.com/HypothesisWorks/hypothesis) #testing #property-based #mpl\
Choose to generate diverse test inputs and shrink failures to simpler examples; it complements test runners such as pytest.

**ruff**: [github](https://github.com/astral-sh/ruff) #linting #formatting\
Choose for fast Python linting and formatting in one tool, with rules covering functionality otherwise spread across multiple tools.

The groups above are recommendations, not authorization to install or introduce packages.

When considering a package for recommendation, consult [discouraged-packages.md](references/discouraged-packages.md). Prefer recommending against packages listed there and explain the recorded reasons. These are recommendations, not prohibitions.

## Further reference

The [PyPI homepage](https://pypi.org/) provides package pages with release histories, compatibility requirements, and project links. Consult it when these details are needed to choose or introduce a package.

Do not fetch the homepage for information already covered here.
