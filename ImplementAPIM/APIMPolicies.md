# API Management Policies

Policies let publishers change API behavior through configuration. They are **XML-based statements** executed sequentially on requests/responses, applied inside the gateway.

---

## Policy Configuration Structure

Four sections executed in order:

```xml
<policies>
  <inbound>
    <!-- Applied to the incoming request -->
  </inbound>
  <backend>
    <!-- Applied before forwarding to backend -->
  </backend>
  <outbound>
    <!-- Applied to the response -->
  </outbound>
  <on-error>
    <!-- Applied if an error occurs at any stage -->
  </on-error>
</policies>
```

- On error, remaining steps in inbound/backend/outbound are **skipped** → jumps to `<on-error>`
- Use `context.LastError` to inspect errors; `set-body` to customize error responses

---

## Policy Expressions

C# expressions usable as attribute values or text values in policies:

- **Single statement:** `@(expression)` — e.g., `@(context.User.Id)`
- **Multi-statement block:** `@{ ... return value; }`
- Has access to `context` variable and a subset of .NET Framework types

**Example — add user data to request header:**

```xml
<inbound>
    <base />
    <set-header name="x-request-context-data" exists-action="override">
        <value>@(context.User.Id)</value>
        <value>@(context.Deployment.Region)</value>
    </set-header>
</inbound>
```

---

## Policy Scopes & the `<base />` Element

Policies can be applied at: **Global → Product → API → Operation**

When multiple scopes apply, ordering is controlled by `<base />`:

```xml
<inbound>
    <cross-domain />       <!-- Executes FIRST -->
    <base />               <!-- Inserts broader-scope policies HERE -->
    <find-and-replace from="xyz" to="abc" />  <!-- Executes AFTER parent policies -->
</inbound>
```

**Key point:** `<base />` determines where parent-scope policies are inserted in the execution order.

---

## Example — Filter Response Content

Strip JSON properties based on the product (e.g., limit data for "Starter" tier):

```xml
<outbound>
    <base />
    <choose>
      <when condition="@(context.Response.StatusCode == 200 && context.Product.Name.Equals(&quot;Starter&quot;))">
        <set-body>
          @{
            var response = context.Response.Body.As<JObject>();
            foreach (var key in new [] {"minutely", "hourly", "daily", "flags"}) {
              response.Property(key).Remove();
            }
            return response.ToString();
          }
        </set-body>
      </when>
    </choose>
</outbound>
```

---

## Advanced Policies

### Control Flow (`<choose>`)

Conditional logic (if-then-else / switch):

```xml
<choose>
    <when condition="Boolean expression">
        <!-- policies if true -->
    </when>
    <when condition="Boolean expression">
        <!-- policies if true -->
    </when>
    <otherwise>
        <!-- policies if all conditions are false -->
    </otherwise>
</choose>
```

- Must have at least one `<when>` element; `<otherwise>` is optional
- Conditions evaluated **in order**; first match wins

### Forward Request

Forwards the request to the backend service. **Removing this policy stops the request from reaching the backend.**

```xml
<forward-request timeout="time in seconds" follow-redirects="true | false"/>
```

- Backend URL set in API settings or overridden with `set-backend-service` policy
- Without it, outbound policies execute immediately after inbound

### Limit Concurrency

Caps concurrent executions; excess requests get **429 Too Many Requests**:

```xml
<limit-concurrency key="expression" max-count="number">
    <!-- nested policies -->
</limit-concurrency>
```

### Log to Event Hubs

Sends request/response context info to an event hub for analysis:

```xml
<log-to-eventhub logger-id="id" partition-id="index" partition-key="value">
  Expression returning a string to be logged
</log-to-eventhub>
```

### Mock Response

Aborts pipeline and returns a mocked response (useful for testing):

```xml
<mock-response status-code="code" content-type="media type"/>
```

- Returns highest fidelity: **examples > schemas > empty body**

### Retry

Re-executes child policies until condition is false or count exhausted:

```xml
<retry condition="boolean" count="number" interval="seconds"
       max-interval="seconds" delta="seconds" first-fast-retry="boolean">
    <!-- child policies -->
</retry>
```

### Return Response

Aborts pipeline and returns a default or custom response:

```xml
<return-response response-variable-name="existing context variable">
  <set-header/>
  <set-body/>
  <set-status/>
</return-response>
```

- Default: **200 OK** with no body
- Custom response via context variable or policy statements (or both)

---

## Quick Recall

| Concept | Key Point |
|---|---|
| Policy format | XML with 4 sections: inbound, backend, outbound, on-error |
| On error | Skips remaining steps, jumps to `<on-error>` |
| Expressions | C# via `@()` or `@{}`, access `context` variable |
| `<base />` | Controls where parent-scope policies execute in the chain |
| Scopes | Global → Product → API → Operation (broadest to narrowest) |
| `<choose>` | Conditional execution (if/else), first true `<when>` wins |
| `<forward-request>` | Sends request to backend; removing it skips backend entirely |
| `<limit-concurrency>` | Caps concurrent requests; excess → 429 |
| `<mock-response>` | Returns fake response, aborts pipeline |
| `<retry>` | Re-executes child policies on failure with configurable intervals |
| `<return-response>` | Aborts pipeline, returns custom/default response |
