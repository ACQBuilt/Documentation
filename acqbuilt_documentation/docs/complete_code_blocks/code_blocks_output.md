# SimphonyWeb Output JSON Specifications

## Introduction

The JSON output specification contains the response generated from the simulation run. 

### data

This is the JSON object which contains the complete response from the simulation engine. The following attributes are response from the simulation run.

- model_id
- models
- resource_utilization
- crew_file_length_list
- crew_waiting_time_list
- error_list_contents

> sample simulation output specifications

```json
{
  "status": "true",
  "messsage": "Simulation run successful",
  "data": {
    "simulate": {
      "model_id": "fj34hf32jf_43ndsfj_r2k4h4indh",
      "models": [
        {
          "actual_start": "4/11/2023 8:00:00 AM",
          "actual_finish": "4/12/2023 12:00:00 PM",
          "duration": "12:00:00",
          "product_name": "spool001",
          "task_name": "cut_task",
          "task_workflow_name": "cut_task_workflow"
        },
        {
          "actual_start": "4/12/2023 1:00:00 PM",
          "actual_finish": "4/13/2023 4:00:00 PM",
          "duration": "11:00:00",
          "product_name": "spool001",
          "task_name": "smooth_task",
          "task_workflow_name": "cut_task_workflow"
        },
        {
          "actual_start": "4/13/2023 4:00:00 PM",
          "actual_finish": "4/13/2023 5:00:00 PM",
          "duration": "01:00:00",
          "product_name": "spool001",
          "task_name": "smooth_task",
          "task_workflow_name": "cut_task_workflow"
        }
      ],
      "resource_utilization": [
        {
          "date_time": "4/11/2023 12:00:00 AM",
          "total": 10,
          "in_use": 0,
          "resource_name": "cut_resource"
        },
        {
          "date_time": "4/11/2023 8:00:00 AM",
          "total": 10,
          "in_use": 7,
          "resource_name": "cut_resource"
        },
        {
          "date_time": "4/12/2023 12:00:00 PM",
          "total": 10,
          "in_use": 0,
          "resource_name": "cut_resource"
        },
        {
          "date_time": "4/12/2023 1:00:00 PM",
          "total": 10,
          "in_use": 7,
          "resource_name": "cut_resource"
        },
        {
          "date_time": "4/13/2023 5:00:00 PM",
          "total": 10,
          "in_use": 0,
          "resource_name": "cut_resource"
        }
      ],
      "crew_file_length_list": [
        {
          "date_time": "4/11/2023 8:00:00 AM",
          "file_length": 0,
          "crew_name": "cut_crew"
        },
        {
          "date_time": "4/13/2023 5:00:00 PM",
          "file_length": 0,
          "crew_name": "cut_crew"
        }
      ],
      "crew_waiting_time_list": [
        {
          "waiting_time": "00:00:00",
          "crew_name": "cut_crew",
          "task_name": "cut_task",
          "product_name": "spool001"
        },
        {
          "waiting_time": "00:00:00",
          "crew_name": "cut_crew",
          "task_name": "smooth_task",
          "product_name": "spool001"
        },
        {
          "waiting_time": "00:00:00",
          "crew_name": "cut_crew",
          "task_name": "smooth_task",
          "product_name": "spool001"
        }
      ],
      "error_list": [
        {
          "entity_categ": "SimulationRun",
          "error_message": "All test passed"
        }
      ]
    }
  }
}
```

### model_id 

This is the same value of the modelid passed during the simulation input process. 

>> datatype : string

### models 

This is a JSON list which contains response about the simulation activity. It contains the attributes listed below

>> datatype : JSON list

 -  actual_start
 - actual_finish
 - duration
 - product_name
 - task_name
 - task_workflow_name

> actual_start : This response shows the actual start time of an activity or task workflow associated with a specific task.
 
  >> datatype : string

> actual_finish : This response shows the actual finish time of an activity or task workflow associated with a specific task.
  
  >> datatype : string

> duration : This response shows the duration it took to complete a specific task
  
  >> datatype : string

> product_name : This response shows the product name that this task was part of to proudce.
  
  >> datatype : string

> task_name : This response shows the task name associated with the workflow
  
  >> datatype : string

> task_workflow_name : This response shows the task_workflow_name associated with the product being simulated
  
  >> datatype : string

> sample models JSON specification 

```json
"models" : [
    {
        "actual_start" : "2023-03-03 8:00:00",
        "actual_finish" : "2023-03-03 15:00:00",
        "duration"      : "06:00:00",
        "product_name"  : "spool001",
        "task_name"     : "cut_task",
        "task_workflow_name" : "Cut Task Workflow"
    }
]
```

### resource_utilization

This is a JSON list which contains response about the resource utilization of the simulation. It contains the following attributes listed below

 > datatype : JSON List

 - date_time
 - total
 - in_use
 - resource_name

 > date_time : This response contains the datetime of the resource utilization in our simulation

  >> datatype : string


 > total : This response contains the total resource available at the specific time. This is useful for the plot in the front end

  >> datatype : double


 > in_use : This response contains the total resource in use at the specific time. This is useful for the plot in the front end

  >> datatype : double

 > resource_name : This response contains the name of the resource that is being used at the specified time
  
  >> datatype : string

> sample resource_utilization JSON specification

```json

"resource_utilization" : [
    {
        "date_time" : "2023-03-22 00:00:00",
        "total" : 10,
        "in_use" : 5,
        "resource_name" : "Cut Resource"
    }
]
```

### crew_file_length_list

This is a JSON list which contains the response of the crew file length list. The following attributes are included in the response.

> datatype : JSON List

 - date_time
 - file_length
 - crew_name

 > date_time : This is the date time of the crew file length. 
  
  >> datatype : string

> file_length : This is the distance of the file. 

 >> datatype : int

> crew_name : This is the name of the crew

 >> datatype : string

```json
"crew_file_length_list" : [
    {
        "date_time" : "2023-03-28 08:00:00",
        "file_length" : 1,
        "crew_name" : "cut_crew"
    }
] 
```
### crew_waiting_time_list

This is the JSON list that stores response of the waiting time of the crew. The following attributes are contents of the list
> datatype : JSON List

- waiting_time
- crew_name
- task_name
- product_name

> waiting_time : This is the waittime of a crew.
 
 >> datatype : string

> crew_name : This is the name of the crew

 >> datatype : string
 
> task_name : This is the name of the task

 >> datatype : string

> product_name : This is the name of the product

 >> datatype : string

> sample JSON crew_waiting_time_list

```json
"crew_waiting_time_list" : [
    {
        "waiting_time" : "16:00:00",
        "crew_name"    : "cut_crew",
        "task_name"    : "cut_task",
        "product_name" : "spool001"
    }
]
```
