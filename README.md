
fetch dt.synthetic.events
| filter dt.synthetic.monitor.id == "Middleware - Sterling File Gateway"
| filter event.type == "http_step_execution"
| fields step.name, result.state
| filter result.state == "SUCCESS"
| summarize success = count(), by: { step.name }
| fields step.name, success_rate = success
| sort success_rate desc
