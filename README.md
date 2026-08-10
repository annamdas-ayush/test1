timeseries availability = avg(dt.synthetic.http.availability),
  by: { dt.entity.http_check, step.name, dt.entity.http_check_step }
| filter matchesValue(entityName(dt.entity.http_check), "Middleware - Sterling File Gateway")
| summarize availability = avg(arrayAvg(availability)), by: { step.name }
| sort availability asc
