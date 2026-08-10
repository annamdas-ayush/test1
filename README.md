timeseries availability = avg(dt.synthetic.http.availability),
  by: { dt.entity.http_check_step, step.name, dt.entity.http_check }
| filter dt.entity.http_check == "Middleware - Sterling File Gateway"
| fieldsAdd step_name = entityName(dt.entity.http_check_step)
| summarize availability = avg(arrayAvg(availability)), by: { step_name }
| sort availability asc
