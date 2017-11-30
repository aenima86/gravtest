---
title: Error object
taxonomy:
    category: docs
---

 
##### Description: 
If NIS encounters an error due to either invalid requests or internal problems, it returns a JSON error object. The interpretation of the error object is dependant on the context. See Appendix B: NIS Errors for detailed information about possible errors. 

 
##### JSON structure by example 
```json
{
        "timeStamp": 9108808,
        "error": "Bad Request",
        "message": "address must be valid",
        "status": 400
        }
``` 
##### Description of the fields: 

| Parameter | Description |
|------|------|
| timeStamp | The number of seconds elapsed since the creation of the nemesis block. |
| error | The general description of the error. |
| message | The detailed error message. |
| Status | The HTTP status. |

 
