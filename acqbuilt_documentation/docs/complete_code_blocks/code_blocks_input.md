# SimphonyWeb INPUT JSON Specifications

## Introduction

SimphonyWeb is a microservice that embedes a couple of components that enables the running of SimphonyDynamic Simulation on the web. The service uses the simulate endpoint. [endpoint](https://simphonywebapp.azurewebsites.net/swagger/index.html/simulation/simulate) to achieve this

## simulate

This is the endpoint used for capturing various components and activity flow needed to run a simulation in the front end. This is seen as the simulation json input in the json schema.

> sample simulation_input JSON schema

```json
{
  "modelid": "string",
  "model_configs": {
    "pointA": "string",
    "pointB": "string"
  },
  "resources": [
    {
      "resource_name": "string",
      "availability": [
        {
          "quantity": 0,
          "from": "string"
        }
      ]
    }
  ],
  "crews": [
    {
      "crew_name": "string",
      "crew_resources": [
        {
          "quantity": 0,
          "resource_name": "string"
        }
      ]
    }
  ],
  "tasks_workflows": [
    {
      "task_workflow_name": "string",
      "tasks": [
        {
          "task_name": "string",
          "task_productivity": 0.0,
          "task_crew": "string"
        }
      ],
      "tasks_connections": [
        {
          "predecessor": "string",
          "successor": "string",
          "finish_to_start_lag": "string",
          "start_to_start_lag": "string",
          "finish_to_finish_lag": "string"
        }
      ]
    }
  ],
  "products": {
    "prod_root_name": "string",
    "products": [
      {
        "product_name": "string",
        "product_quantity": 0.0,
        "task_workflow_name": "string"
      }
    ]
  }
}
```
> simulation input with values

```json
{
  "modelid": "fj34hf32jf_43ndsfj_r2k4h4indh",
  "model_configs": {
    "pointA": "2023-04-10",
    "pointB": "2023-04-11"
  },
  "resources": [
    {
      "resource_name": "cut_resource",
      "availability": [
        {
          "quantity": 10,
          "from": "2023-04-10"
        }
      ]
    }
  ],
  "crews": [
    {
      "crew_name": "cut_crew",
      "crew_resources": [
        {
          "quantity": 7,
          "resource_name": "cut_resource"
        }
      ]
    }
  ],
  "tasks_workflows": [
    {
      "task_workflow_name": "cut_task_workflow",
      "tasks": [
        {
          "task_name": "cut_task",
          "task_productivity": 2,
          "task_crew": "cut_crew"
        },
        {
          "task_name": "smooth_task",
          "task_productivity": 2,
          "task_crew": "cut_crew"
        }
      ],
      "task_connections": [
        {
          "predecessor": "cut_task",
          "successor": "smooth_task",
          "finish_to_start_lag": "01:00:00",
          "start_to_start_lag": "01:00:00",
          "finish_to_finish_lag": "01:00:00"
        }
      ]
    }
  ],
  "products": {
    "prod_root_name": "root",
    "products": [
      {
        "product_name": "spool001",
        "product_quantity": 24,
        "task_workflow_name": "cut_task_workflow"
      }
    ]
  }
}
```

### modelid

modelid is a string value auto-generated in the front end of SimphonyWeb. 

> datatype : string

> sample model_id specifications

```json
{
  "modelid": "38jd920js0-_dji301dn_hdj390jjs"
```

### model_configs

model_configs is a JSON object that contains attributes that are used at the top-level for running the simulation. The attributes are listed below

  >> datatype : JSON Object

- pointA
- pointB

> pointA : This is usually a datetime value which represents the scheduled start time of the simulation.

  >> datatype : string

> pointB : This is also a datetime value which represents the current time of the simulation.
 
  >> datatype : string

 These values are passed as a string in the JSON schema and then converted to a datetime usually sent to the engine. Find samples of the various values below.

 > sample model_configs json specification

 ```json
 "model_configs" : {
  "pointA" : "2023-03-04",
  "pointB" : "2023-04-04"
 }
```
### resources

This is a JSON list that holds the skilled personnel, equipments or various utilities needed to run the simulation.This schema contains the following attributes listed below

> datatype : JSON List

- resource_name
- availability

> resource_name : This is the name of the type of skilled personnel, equipments or utilities needed for a simulation project. This has a datatype of string.

  >> datatype : string

> availability : This is a JSON list schema that holds values which defines the availability of these resources. The following attributes are listed below as the availability properties

  >> datatype : string

  - quantity
  - from

  >> quantity : This is the number of resource that is available for the simulation. 

    >>> datatype : integer

  >> from : This is a value that defines the time the resources will be available. This is captured as a string in the JSON schema but internally converted to a datetime in the api.

    >>> datatype : string

> resources sample specification

```json
"resources" : [
  {
    "resource_name" : "Cut Resources",
    "availability" : [
      {
        "quantity" : 10,
        "from" : "2023-03-04"
      }
    ]
  }
]
```

### crews

Crews are JSON list schemas that are used for collating various resources together needed for running a simulation for a project. It contains the following attributes listed below.

- crew_name
- crew_resources

> crew_name : This is used the define the name of a single crew. 

  >> datatype : string

> crew_resources : This is a json list schema which defines the attributes needed for collating resources together for a simulation project.
It contains the following attributes 
  
  - quantity
  - resource_name

  >> quantity : This defines the number of resources needed by the crew to carry out the task. 

    >>> datatype : string
  
  >> resource_name : This is the value that points to the name of the resources created earlier. This internally links to resource object needed for the simulation. 

    >>> datatype : string

> sample crew specification

```json
"crews" : [
  {
    "crew_name" : "Cut Crew",
    "crew_resources" : [
      {
        "quantity" : 5,
        "resource_name" : "Cut Resources"
      }
    ]
  }
]
```
### tasks_workflows

This is the JSON schema that defines the various tasks workflow needed for a simulation run. It contains the following attributes as listed below.

> datatype : JSON list

- task_workflow_name
- tasks
- tasks_connections

> task_workflow_name : This is the value that defines the name of a single workflow in the simulation run. 

  >> datatype : string

> tasks : This is a JSON list that defines the various tasks associated with a task workflow. This contains the follwing attributes as listed below

  >> datatype : JSON list

  - task_name
  - task_productivity
  - task_crew

  >> task_name : This is a value that defines the name of single task.
   
   >>> datatype : string
  
  >> task_productivity : This is a value that defines the number of hours it takes to produce a single unit of an endproduct. Internally this value is embedded in the Constant Distribution productivity. 

    >>> datatype : double

  >> task_crew : This is a value that associates a crew to a task. This points to the crew needed to carry out a specific task in the simulation run. 

    >>> datatype : string

> tasks_connections : This is a JSON list which defines the various orders or flows of a specific workflow. This contains the following attributes as listed below.

  - predecessor
  - successor
  - finish_to_start_lag
  - start_to_start_lag
  - finish_to_finish_lag

  >> predecessor : This is value that defines the preceding task in the workflow. This usually associates the task already created.
    
    >>> datatype : string
  
  >> successor : This is the value that defines the succeeding task in the workflow. This is usually associated with a task created earlier.

    >>> datatype : string

  >> finish_to_start_lag : This the value that defines the lag for the finish to start activity. The value is captured internally in the api as a timespan format.

    >>> datatype : string
  
  >> start_to_start_lag : This the value that defines the lag for the start to start activity. The value is captured internally in the api as a timespan format.

    >>> datatype : string
  
  >> finish_to_finish_lag : This the value that defines the lag for the finish to finish activity. The value is captured internally in the api as a timespan format.

    >>> datatype : string


> sample tasks_work_flows specifications

```json
"tasks_workflows" : [
  {
    "task_workflow_name" : "Cut Task Workflow",
    "tasks" : [
      {
        "task_name" : "Cut Task",
        "task_productivity" : 2.0,
        "task_crew" : "Cut Crew"
      },
      {
        "task_name" : "Smooth Task",
        "task_productivity" : 4.0,
        "task_crew" : "Cut Crew"
      }
    ],
    "tasks_connections" : [
      {
        "predecessor" : "Cut Task",
        "successor" : "Smooth Task",
        "finish_to_start_lag" : "01:00:00",
        "start_to_start_lag"  : "01:00:00",
        "finish_to_start_lag" : "01:00:00"
      }
    ]
  }
]
```

### products

Products is a JSON list that defines the project we wish to simulate. These includes the templates associated with each product to successfully run a simulation. The products contains two fields as listed below.

> datatype : JSON object

  - prod_root_name
  - products

> prod_root_name : This is the value that defines the root name of the product
  
  >> datatype : string

> products : This is the JSON list value that defines the actual product we wish to simulate. It contains the following attributes as listed below

  >> datatype : JSON list

  - product_name
  - product_quantity
  - task_workflow

  >> product_name : This is the value used to define the name of a single product

    >>> datatype : string

  >> product_quantity : This is the value used to define the total number of products the simulation engine will produce in the simulation process. 

    >>> datatype : double
  
  >> task_workflow : This is the value that holds the task workflow used for simulating a product. This usually associates with an existing task work flow
    
    >>> datatype : string
  
  > sample products specification

```json
"products" : {
  "prod_root_name" : "root",
  "products" : [
    {
      "product_name" : "Spool001",
      "product_quantity" : 24.0,
      "task_workflow" : "Cut Task Workflow"
    }
  ]
}

```

