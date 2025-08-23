## Scale apps in Azure App service

### Intro

Autoscaling in for Azure Webapps and more azure resources, 
Autoscaling requires to configure autoscale rules that specify the conditions under which resources should be added or removed.


LO:

- Scenarios for which autoscaling is an appropriate solution
- Rules for a web app
- Understand the effects of autoscaling 

---

### Scale Out Options

#### Scaling Methods
Azure App Service supports three scaling approaches:
- **Manual Scaling**: Direct control over instance count
- **Autoscaling with Azure Autoscale**: Rule-based scaling decisions
- **Azure App Service Automatic Scaling**: Platform-managed scaling

#### Comparison: Autoscale vs Automatic Scaling

| Factor | Autoscale | Automatic Scaling |
|--------|-----------|-------------------|
| **Pricing Tiers** | Standard and Up | Premium V2 (P1V2-P3V2), Premium V3 (P0V3-P5MV3) |
| **Rule-based** | Yes | No (platform-managed via HTTP traffic) |
| **Schedule-based** | Yes | No |
| **Always Ready Instances** | No | Yes (minimum 1) |
| **Prewarmed Instances** | No | Yes (default 1) |
| **Per-app Maximum** | No | Yes |

### Autoscaling Concepts

#### What is Autoscaling?
- **Definition**: Cloud process that adjusts resources based on current demand
- **Direction**: Scales in/out (not up/down)
- **Triggers**: Schedule-based or resource metrics (CPU, memory, requests)
- **Response**: Adds/removes web servers and balances load

#### Autoscaling Rules
- **Rule-based Decisions**: Define thresholds for metrics
- **Threshold Crossing**: Triggers scaling events
- **Resource Deallocation**: Removes resources when workload decreases
- **Careful Definition**: Avoid scaling during DoS attacks

### When to Use Autoscaling

#### Ideal Scenarios
- **Predictable Patterns**: Business apps with holiday traffic variations
- **Availability Improvement**: Ensures requests aren't denied
- **Fault Tolerance**: Handles instance crashes gracefully
- **Elastic Workloads**: Variable demand applications

#### When NOT to Use Autoscaling
- **Resource-intensive Processing**: Single requests exhaust instance capacity
- **Long-term Growth**: Predictable growth better handled manually
- **Few Instances**: Limited initial capacity affects scaling effectiveness
- **DoS Vulnerability**: Can be exploited by malicious traffic

#### Cost Considerations
- **Monitoring Overhead**: Resource monitoring costs
- **Manual Alternative**: May be more cost-effective for predictable growth
- **Scaling Delays**: Time needed to spin up new instances

### Azure App Service Automatic Scaling

#### Configuration
- **App Service Plan Level**: Enable for entire plan
- **Instance Range**: Configure min/max instances per web app
- **HTTP Traffic Monitoring**: Platform monitors load automatically
- **Independent Scaling**: Apps scale differently within same plan

#### Use Cases
- **No Rule Configuration**: Don't want to set up autoscale rules
- **Independent App Scaling**: Different scaling needs per app
- **Backend Protection**: Prevent overwhelming databases/legacy systems
- **Maximum Instance Limits**: Control scaling bounds

#### Key Features
- **Automatic Load Monitoring**: Platform handles HTTP traffic analysis
- **Resource Sharing**: Multiple apps can scale simultaneously
- **Backend Consideration**: Protects slower-scaling backend systems
- **Instance Management**: Platform manages instance lifecycle

### Best Practices
- **Define Clear Rules**: Avoid unnecessary scaling events
- **Consider Backend Limits**: Ensure dependent systems can handle scale
- **Monitor Costs**: Balance performance with cost efficiency
- **Plan for Growth**: Choose appropriate scaling strategy for workload type
- **Test Scenarios**: Validate scaling behavior under different conditions

---

### Autoscale Factors & Configuration

#### Autoscaling and App Service Plan
- **Feature Level**: Autoscaling is an App Service Plan feature
- **Hardware Scaling**: Starts new instances of defined hardware
- **Instance Limits**: Each pricing tier has maximum instance limits
- **Pricing Dependency**: Not all pricing tiers support autoscaling
- **Cost Management**: Higher tiers have higher instance limits

#### Autoscale Conditions

**Two Primary Options:**
1. **Metric-based Scaling**: Based on resource metrics (CPU, memory, requests)
2. **Schedule-based Scaling**: Scale to specific instance count at defined times

**Condition Types:**
- **Combined Conditions**: Metric + schedule (e.g., scale on HTTP requests only during business hours)
- **Multiple Conditions**: Azure scales when ANY condition applies
- **Default Condition**: Always active when no other conditions apply

#### Autoscale Metrics

| Metric | Description | Use Case |
|--------|-------------|----------|
| **CPU Percentage** | CPU utilization across all instances | Detect CPU-bound scenarios |
| **Memory Percentage** | Memory occupancy across instances | Prevent memory exhaustion |
| **Disk Queue Length** | Outstanding I/O requests count | Identify disk contention |
| **HTTP Queue Length** | Pending client requests | Prevent HTTP 408 timeout errors |
| **Data In** | Bytes received across instances | Monitor incoming traffic |
| **Data Out** | Bytes sent by instances | Monitor outgoing traffic |

**External Metrics**: Can scale based on other Azure service metrics

#### Metric Analysis Process

**Step 1: Time Grain Aggregation**
- **Period**: Usually 1 minute (intrinsic to each metric)
- **Aggregation Options**: Average, Minimum, Maximum, Sum, Last, Count
- **Purpose**: Collect initial metric values

**Step 2: Duration Aggregation**
- **Minimum Duration**: 5 minutes
- **Purpose**: Analyze trends over longer periods
- **Example**: 10-minute duration aggregates 10 one-minute values
- **Different Calculation**: Can use different aggregation method than time grain

#### Autoscale Actions

**Action Types:**
- **Scale-out**: Increase instance count (typically uses "greater than" operator)
- **Scale-in**: Decrease instance count (typically uses "less than" operator)
- **Set Specific Count**: Scale to exact instance number

**Cool Down Period:**
- **Minimum**: 5 minutes
- **Purpose**: Allow system stabilization between scaling events
- **Consideration**: Instance startup/shutdown time affects metric visibility

#### Rule Configuration Best Practices

**Pairing Rules:**
- **Scale-out Rule**: Define upper threshold for scaling out
- **Scale-in Rule**: Define lower threshold for scaling in
- **Same Condition**: Include both rules in same autoscale condition
- **Different Thresholds**: Prevent constant scaling (hysteresis)

**Combining Rules:**
- **Multiple Scale-out**: Scale if ANY scale-out rule triggers
- **Multiple Scale-in**: Scale only if ALL scale-in rules are met
- **Separate Conditions**: Use different conditions for OR logic on scale-in

**Example Rule Combination:**
```
Scale-out Rules (ANY triggers action):
- HTTP queue length > 10: Scale out by 1
- CPU utilization > 70%: Scale out by 1

Scale-in Rules (ALL must be met):
- HTTP queue length = 0: Scale in by 1
- CPU utilization < 50%: Scale in by 1
```

#### Key Considerations
- **Threshold Planning**: Avoid too aggressive scaling with proper threshold gaps
- **Metric Selection**: Choose metrics that best represent application load
- **Rule Logic**: Understand AND vs OR logic for multiple rules
- **Stabilization**: Allow sufficient cool down periods
- **Cost Impact**: Balance responsiveness with cost efficiency
- **Testing**: Validate autoscale behavior under various load conditions

