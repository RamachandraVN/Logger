# Logger

A simple and configurable Swift logging system for iOS, macOS, and Swift projects. RVNLogger provides a flexible logging solution with support for multiple log levels, output formats, and destinations. Console logging is always enabled, while file and remote logging are optional.

- **Log to console, file, and/or remote HTTP endpoint**
- **Choose between text and JSON output formats**
- **Configurable log levels: debug, warning, error**
- **Thread-safe and efficient buffering**
- **Easy to integrate with Swift Package Manager**

## Features

- **Log Levels:**
  - `debug` (🛠): For detailed information during development
  - `warning` (⚠️): For potentially harmful situations
  - `error` (❌): For serious problems that need attention
- **Output Formats:**
  - `.text`: Human-readable format with emojis and timestamps
  - `.json`: Machine-readable format suitable for log aggregation and analysis
- **Performance & Safety:**
  - Console logging is synchronous and thread-safe
  - File and remote logging are asynchronous and thread-safe
  - Automatic buffer flushing on deallocation
  - Weak self references in async blocks
  - Configurable buffer size to control memory usage

## Usage

### Basic Usage

```swift
import Logger

let logger = RVNLogger()
logger.debug("Processing started")
logger.warning("High memory usage")
logger.error("Connection failed")
```

### Log Level Examples & Output

```swift
logger.debug("This is a debug message")      // 🛠 For detailed information during development
logger.warning("This is a warning message")  // ⚠️ For potentially harmful situations
logger.error("This is an error message")     // ❌ For serious problems that need attention
```

**Console Output (text format):**
```
2024-03-21 10:30:45.123 [🛠] [MyFile.swift:myFunction] This is a debug message
2024-03-21 10:30:45.124 [⚠️] [MyFile.swift:myFunction] This is a warning message
2024-03-21 10:30:45.125 [❌] [MyFile.swift:myFunction] This is an error message
```

**Console Output (JSON format):**
```
{"timestamp":"2024-03-21 10:30:45.123","level":"0","file":"MyFile.swift","function":"myFunction","message":"This is a debug message"}
{"timestamp":"2024-03-21 10:30:45.124","level":"1","file":"MyFile.swift","function":"myFunction","message":"This is a warning message"}
{"timestamp":"2024-03-21 10:30:45.125","level":"2","file":"MyFile.swift","function":"myFunction","message":"This is an error message"}
```

### Logging to File and Remote for LogAnalysis

RVNLogger can log to the console, a file, and/or a remote HTTP endpoint simultaneously. Just set the appropriate properties in your configuration:

```swift
import Logger

var config = RVNLoggerConfig()
config.logFormat = .json
config.fileURL = URL(fileURLWithPath: "/tmp/app.log")
config.remoteURL = "https://your-log-endpoint.example.com/logs"

let logger = RVNLogger(config: config)
logger.error("Critical failure: disk full!")
```

**File Output (`/tmp/app.log`):**
```
{"timestamp":"2024-03-21 10:31:00.000","level":"2","file":"MyFile.swift","function":"myFunction","message":"Critical failure: disk full!"}
```

**Remote Output:**
- The same JSON payload is sent as an HTTP POST to your remote URL.

> **Note:**
> For more advanced usage, configuration options, and log format examples, see the documentation in [`Logger/RVNLogger.swift`](Logger/RVNLogger.swift).

## Requirements
- iOS 13.0+ / macOS 10.15+
- Swift 5.7+

## License
MIT 
