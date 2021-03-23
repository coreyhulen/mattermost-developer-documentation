---
title: "Go Style Guide"
date: 2021-01-12T16:00:00+0530
weight: 3
subsection: Server
---

Go is a more opinionated language than many others when it comes to coding style. The compiler enforces some basic stylistic elements, such as the removal of unused variables and imports. Many others are enforced by the `gofmt` tool, such as usage of white-space, semicolons, indentation, and alignment. The `gofmt` tool is run over all code in the Mattermost Server CI pipeline. Any code which is not consistent with the formatting enforced by `gofmt` will not be accepted into the repository.

Despite this, there are still many areas of coding style which are not dictated by these tools. Rather than reinventing the wheel, we are adopting [Effective Go](https://golang.org/doc/effective_go.html) as a basis for our style guide. On top of that, we also follow the guidelines laid out by the Go project at [CodeReviewComments](https://github.com/golang/go/wiki/CodeReviewComments).

However, at present, some of the guidelines from these sources come into conflict with existing patterns that are present in our codebase which cannot immediately be corrected due to the need to maintain backward compatibility.

This document, which should be read in conjunction with [Effective Go](https://golang.org/doc/effective_go.html) and [CodeReviewComments](https://github.com/golang/go/wiki/CodeReviewComments), outlines the small number of exceptions we make to maintain backward compatibility, as well as a number of additional stylistic rules we have adopted on top of those external recommendations.

### Model package

The `model` package is our public API which is consumed by many plugins and third-party integrations. The need to maintain backward compatibility for these external users of the `model` package prevents us from immediately bringing it into compliance with some of the rules outlined in this document.

In order to avoid delaying the adoption of these rules in the wider codebase, we have chosen to temporarily exempt only the `model` package from certain rules (indicated below). However, outside of the `model` package, these rules should be followed in all new or modified code.

### Application of guidelines

In addition to the specific exceptions made for backward compatibility in the `model` package, all new commits should also follow the rules as outlined in this and the linked documents, for both new and modified code.

This does not, however, mean that a developer is *required* to fix any surrounding code that contravenes the rules in the style guide. It's encouraged to keep fixing things as you go, but it is not compulsory to do so. Reviewers should refrain from asking for stylistic changes in surrounding code if the submitter has not included them in their pull request.

## Guidelines

### Functional

#### Default to sync instead of async

Always prefer synchronous functions by default. Async calls are hard to get right. They have no control over goroutine lifetimes and introduce data races. If you think something needs to be asynchronous, measure it and prove it. Ask these questions:

- Does it improve performance? If so, by how much?
- What’s the tradeoff of the happy path vs. slow path?
- How do I propagate errors?
- What about back-pressure?
- What should be my concurrency model?

Do not create one-off goroutines without knowing when/how they exit. They cause problems that are hard to debug, and can often cause performance degradation rather than an improvement. Have a look at:

- https://github.com/golang/go/wiki/CodeReviewComments#goroutine-lifetimes
- https://github.com/golang/go/wiki/CodeReviewComments#synchronous-functions

#### Pointers to slices

Do not use pointers to slices. Slices are already reference types which point to an underlying array. If you want a function to modify a slice, then return that slice from the function, rather than passing a pointer.

This rule is not yet fully applied to the `model` package due to backward compatibility requirements.

#### Avoid creating more ToJSON methods

Do not create new `ToJSON` methods for model structs. Instead, just use `json.Marshal` at the call site. This has two major benefits:

- It avoids bugs due to the suppression of the JSON error which happens with `ToJSON` methods (we've had a number of bugs caused by this).
- It's a common pattern to pass the output to something (like a network call) which accepts a byte-slice, leading to a double conversion from byte-slice to string to a byte-slice again if `ToJSON` methods are used.

#### [Interfaces](https://github.com/golang/go/wiki/CodeReviewComments#interfaces)

- Return structs, accept interfaces.
- Interface names should end with “-er”. This is not a strict rule. Just a guideline which indicates the fact that interface functionalities are designed around the concept of “doing” something.
- Try not to define interfaces on the implementer side of an API "for mocking"; instead, design the API so that it can be tested using the public API of the real implementation.

As an example, if you're trying to integrate with a third-party service, it's tempting to create an interface and use that in the code so that it can be easily mocked in the test. This is an anti-pattern and masks real bugs. Instead, you should try to use the real implementation via a docker container or if that's not feasible, mock the network response coming from the external process.

Another common pattern is to preemptively declare the interface in the source package itself, so that the consumer can just directly import the interface. Instead, try to declare the interface in the package which is going to consume the functionality. Often, different packages have non-overlapping set of functionalities to consume. If you do find several consumers of the package, remember that interfaces can be composed. So define small chunks of functionalities in different interfaces, and let consumers compose them as needed. Take a look at the set of interfaces in the [io](https://golang.org/pkg/io/) package.

These are just guidelines and not strict rules. Understand your use case and apply them appropriately.

### Stylistic

#### [CamelCase variables/constants](https://github.com/golang/go/wiki/CodeReviewComments#mixed-caps)

We use CamelCase names like WebsocketEventPostEdited, not WEBSOCKET_EVENT_POST_EDITED.

This rule is not yet fully applied to the `model` package due to backward compatibility requirements.

#### Empty string check

Use `foo == ""` to check for empty strings, not `len(foo) == 0`.

#### [Reduce indentation](https://github.com/golang/go/wiki/CodeReviewComments#indent-error-flow)

If there are multiple return statements in an if-else statement, remove the else block and outdent it.

This is an example from `mlog/human/parser.go`:

```go
// Look for an initial "{"
if token, err := dec.Token(); err != nil {
	return result, err
} else {
	d, ok := token.(json.Delim)
	if !ok || d != '{' {
		return result, fmt.Errorf("input is not a JSON object, found: %v", token)
	}
}
```

This can be simplified to:

```go
// Look for an initial "{"
if token, err := dec.Token(); err != nil {
	return result, err
}
d, ok := token.(json.Delim)
if !ok || d != '{' {
	return result, fmt.Errorf("input is not a JSON object, found: %v", token)
}
```

#### [Initialisms](https://github.com/golang/go/wiki/CodeReviewComments#initialisms)

Use `userID` rather than `userId`. Same for abbreviations; `HTTP` is preferred over `Http` or `http`.

This rule is not yet fully applied to the `model` package due to backward compatibility requirements.

#### [Receiver Names](https://github.com/golang/go/wiki/CodeReviewComments#receiver-names)

The name of a method's receiver should be a reflection of its identity; often a one or two letter abbreviation of its type suffices (such as "c" or "cl" for "Client"). Don't use generic names such as "me", "this", or "self" identifiers typical of object-oriented languages that give the variable a special meaning.

### Log levels

The purpose of logging is to provide observability - it enables the application communicate back to the administrator about what is happening. To communicate effectively logs should be meaningful and concise. To achieve this, log lines should conform to one of the definitions below:

**Critical:** This log-level represents the most severe situations when the service is entirely unable to continue operating. After emitting a _critical_ log line, it is expected that the service will terminate.

For example, the code block below demonstrates a _critical_ situation where the server startup routine fails, meaning the service is unable to start and must terminate.

```go
func runServer(..) {
	..
	server, err := app.NewServer(options...)
	if err != nil {
		mlog.Critical(err.Error())
		return
	}
	..
}
```

**Error:** This log-level is used when something unexpected has happened to the service, but it does not result in a total loss of service. Log lines using the _error_ level must be actionable, so that the system administrator can investigate and resolve the incident. The _error_ log level may indicate a loss of service for an individual user or request or it may indicate a total failure of a non-critical subsystem within the service.

For example, the _error_ log level is used in the code snippet below as it represents a partial failure of one non-critical subsystem of the service. Administrator intervention is required to resolve this situation, but the rest of the service is able to continue operating in the meantime.

```go
func (a *App) SyncPlugins(..) {
	..
	reader, appErr := a.FileReader(plugin.path)
	if appErr != nil {
		mlog.Error("Failed to open plugin bundle from file store.", mlog.String("bundle", plugin.path), mlog.Err(appErr))
		return
	}
	..
}
```

**Warn:** This log level is used to indicate that something unexpected has happened, but the server is able to continue operating and it has not suffered any loss of functionality as a consequence of this failure. System administrators may wish to investigate the cause of log lines at this level, but the need is typically less pressing than for those at _error_ level. System administrators may also wish to monitor the rate of occurrence of individual log-lines at this level as this may be indicative of a wider problem. Log lines at the _warning_ level should be as detailed as possible, since these are often the least clear-cut category of message.

For example, the _warning_ log level may be used to indicate that something went wrong but the overall operation was still able to complete successfully.

```go
func (a *App) UpdateUserRoles(..) {
	..
	if result := <-schan; result.NErr != nil {
		// soft error since the user roles were still updated
		mlog.Warn("Error during updating user roles", mlog.Err(result.NErr))
	}

	a.InvalidateCacheForUser(userId)
	..
}
```

**Info:** This log level should be used to record normal, expected application behavior, even if it results in an error for the end user. They are not actionable individually, but the significant changes in the frequency of occurrence of individual log lines at this level may be indicative of a possible problem.

For example, the _info_ log level may be used to communicate to administrators that certain subsystems within the service have been started or stopped.

```go
func (s *Schedulers) Start(..) {
	s.startOnce.Do(func() {
		mlog.Info("Starting schedulers.")
		..
	})
	..
}
```

**Debug:** This log-level is used for diagnostic information which may be used to debug issues but is not necessary for normal production system logging, nor actionable by system administrators.

```go
func (worker *Worker) Run() {
	mlog.Debug("Worker started", mlog.String("worker", worker.name))
	..
}
```

## Proposing a new rule

To propose a new rule, follow the process below:

- Add it to the agenda in the [Server](https://community.mattermost.com/core/channels/developers-server) Guild meeting, and propose it.
- If it gets accepted, create a go-vet rule (if possible), or a golangci-lint rule to prevent new regressions from creeping in.
- Fix all existing issues.
- Add it to this guide.
