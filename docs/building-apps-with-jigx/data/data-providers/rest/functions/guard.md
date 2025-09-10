# Guard

Guard functions control whether the main function should execute, based on runtime conditions such as query results, server responses, or business logic rules.

A guard function runs after any defined queries and before the main REST call is executed. It can call another function to validate the current app state, perform a check against local or remote data, and return a result that determines whether to proceed with the main function or not.

The outcome of the guard function, whether it succeeds or fails, determines the next steps in your app's flow.

## What guard functions do

* Act as a **pre-check** before executing the main function.
* Help prevent actions under incorrect conditions (e.g., stale data, duplicate submissions).
* Evaluate dynamic conditions based on **local queries**, **app parameters**, or **API responses**.
* Optionally trigger fallback operations if the check fails.

## When to use guard functions

**Technical issues** - Prevent REST calls when a condition already exists—for example, checking if a record already exists on the server to avoid duplicate entries.

**Business Logic** - Verify preconditions, like checking if an appointment is still open before allowing status updates, especially useful in offline-first or multi-device environments.

**Example:** When completing an appointment, a guard function can check if the appointment’s status is still open. If the status has changed to closed on the server, the guard function returns false and shows an error message, preventing invalid updates.

## Execution flow

When used in a function:

1. The guard function is executed first (if enabled for initial/continuation/retry).
2. If the guard succeeds, the main function proceeds as normal.
3. If the guard fails, the main function is skipped, and any defined `operations` in the guard are executed instead.
4. The guard’s output is available using `=@ctx.guard.output`.

## Execution timing options

<table><thead><tr><th width="163.55078125">Property</th><th>Purpose</th></tr></thead><tbody><tr><td><code>onInitial</code></td><td>Runs guard before the initial REST call.</td></tr><tr><td><code>onContinuation</code></td><td>Re-evaluates guard on function continuation.</td></tr><tr><td><code>onRetry</code></td><td>Runs guard before retrying a failed function.</td></tr></tbody></table>

## Guard Output

* Use the `=@ctx.guard.output` expression to get the output from the guard function.
*
* The output is never saved to a table.
* The output can be used when chaining function calls.
* If the output is not explicitly used, the default provider's output is used, and in the case of the REST provider, that would be the body.

## Configuration options

<table><thead><tr><th width="161.26171875">Properties</th><th>Description</th></tr></thead><tbody><tr><td><code>function</code></td><td>The name or <code>functionId</code> of the function to execute as the guard, before the main function, to determine whether the main function should be executed.</td></tr><tr><td><code>Parameters</code></td><td><code>parameters</code> passed to the guard function from the specified <code>function</code>.</td></tr><tr><td><code>onContinuation</code></td><td>Determine if the guard function should be executed on a <code>continuation</code> call. Defaults to <code>true</code>.</td></tr><tr><td><code>onInitial</code></td><td>Determines whether the guard function executes before the first call to the REST function. Default is <code>true</code>. If set to <code>false</code>, the guard function will execute in the defined <a href="./#function-execution-order">execution order</a>.</td></tr><tr><td><code>onRetry</code></td><td>Determines whether the function should execute a retry call.<br>Defaults to <code>true</code>.</td></tr><tr><td><code>operations</code></td><td>Operations to run if the guard function <em>fails</em>. Used to update local data, show messages, or log state.</td></tr><tr><td><code>result</code></td><td>The result of the guard function is evaluated to determine whether the main function should be executed. If the guard function fails or the result of the expression is falsy, the main function is not executed. The output of the guard function is available to expressions and scripts using <code>=@ctx.guard.output</code></td></tr><tr><td><code>when</code></td><td>Condition to determine if the guard function itself should execute.</td></tr></tbody></table>

## Expressions

<table><thead><tr><th width="100.25390625"></th><th width="179.015625">Expression</th><th>Description</th></tr></thead><tbody><tr><td>output</td><td><code>=@ctx.guard.output</code></td><td>Output of the guard function is returned to the function as actions. If specified, the output of the function is the result of the expression; otherwise, the output is defined as the default output of the REST provider.</td></tr></tbody></table>
