---
title: NemAsyncTimerVisitor
taxonomy:
    category: docs
---

 
##### Description: 
NIS uses timers to schedule periodic tasks. Those tasks are monitored and their result is memorized. The NemAsyncTimeVisitor structure holds the information.

 
##### JSON structure by example: 
```json
{
        "last-delay-time": 3000,
        "executions": 1024,
        "failures": 0,
        "successes": 1024,
        "last-operation-start-time": 9317695,
        "is-executing": 0,
        "name": "FORAGING",
        "average-operation-time": 0,
        "last-operation-time": 0
        }
``` 
##### Description of the fields: 

| Parameter | Description |
|------|------|
| last-delay-time | The number of milliseconds since the last execution of the timer. |
| executions | The number of times the task was executed. |
| failures | The number times the task failed. |
| successes | The number times the task was successful. |
| last-operation-start-time | The time at which the task started last time. |
| is-executing | True if the task is executing, false otherwise. |
| name | The name of the task. |
| average-operation-time | The number of seconds the task needed on average. |
| last-operation-time | The number of seconds the task needed the last time. |

 
